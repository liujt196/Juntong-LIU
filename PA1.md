Short destription  
I defined four function: get match score, shift sequence1, shift sequence2, store shifted sequence in list
the get match score function is using a matching_word_count, it is in the loop, when these two sequences have one match word, matching_word_count +1
the shift function is using a list and then insert "-" to the left or right
the store shifted sequence function is using a list to store the shifted sequences
in the main program i used a dictionary to store the match store and the loop count, and then sort the max key value by using max(dict_value, key+dict_value.get)

code
dna1 = input("input dna sequence1")
f = open('dna1.txt', 'w')
f.write(','.join(dna1))
dna2 = input("input dna sequence2")
s = open('dna2.txt', 'w')
s.write(','.join(dna2))
def get_num(s1, s2):
    len_s1 = len(s1)
    matching_word_count = 0
    for i in range(len_s1):
        if s1[i] == s2[i]:
            matching_word_count = matching_word_count + 1
    return matching_word_count
def move_right(lt, n):
    lt = list(lt)
    for i in range(n % len(lt)):
        lt.insert(0, '-')
    return "".join(lt)
def move_left(lt, n):
    lt = list(lt)
    for i in range(n % len(lt)):
        lt.insert(len(lt), '-')
    return "".join(lt)

def f(n):
    shiftlist = []
    for i in range(0,n):
        if n <= len(dna1):
            shiftlist.append(move_right(dna1,i))
            shiftlist.append(move_left(dna2, i))
        else:
            shiftlist.append(move_left(dna1, i))
            shiftlist.append(move_right(dna2, i))
    return shiftlist



list1 = []
dict_value = {}
count = 0
try:
    for i in range(0,len(dna1)):
        move_right(dna1,i)
        move_left(dna2,i)
        get_num(move_right(dna1,i),move_left(dna2,i))
        count += 1
        dict_value.update({count:get_num(move_right(dna1,i),move_left(dna2,i))})
    for i in range(0,len(dna2)):
        move_left(dna1,i)
        move_right(dna2,i)
        get_num(move_left(dna1,i),move_right(dna2,i))
        count += 1
        dict_value.update({count: get_num(move_left(dna1, i), move_right(dna2, i))})
except(IndexError,ValueError):
    print("sequence must have the same length")
except(Exception, ZeroDivisionError):
    print("u cant type empty")

try:
    key_max = max(dict_value, key=dict_value.get)
    a = f(key_max)
    print("maximum chain is " + a[-1])
    print("maximum chain is " + a[-2])
    print("number of matches is " + str(get_num(a[-1],a[-2])))
    if key_max <= len(dna1):
        print("shifting sequence 1 by " + str((key_max) - 1))
    else:
        print("shifting sequence2 by " + str((key_max) - len(dna1) - 1))
except(ValueError):
    print("check your input")


result:
input dna sequence1ACTGATCAC
input dna sequence2TTAGCTCGA
maximum chain is --TTAGCTCGA
maximum chain is ACTGATCAC--
number of matches is 4
shifting sequence2 by 2
A,C,T,G,A,T,C,A,C
T,T,A,G,C,T,C,G,A



input dna sequence1dawdawda
input dna sequence2da
sequence must have the same length
check your input
d,a,w,d,a,w,d,a
d,a


input dna sequence1dadwada
input dna sequence2
u cant type empty
check your input
d,a,d,w,a,d,a


input dna sequence1qxsawzx
input dna sequence2zxaswqz
maximum chain is zxaswqz
maximum chain is qxsawzx
number of matches is 2
shifting sequence 1 by 0
q,x,s,a,w,z,x
z,x,a,s,w,q,z

