I have the sketched process:

head in initial character
check the character at head
if it is 'u': mark (u -> u'):
	sweep to the right
	'd' found, mark (d -> d') and move head to beginning
	'd' not found $\iff$ ' ' (space) found: reject
is it is ' ' (a space) move head to beginning
check char in head
if it is 'r', mark (r -> r')
	sweep head to the right
	if 'l' found, mark (l -> l') and move head to beginning
	if 'l' not found $\iff$ ' ' (space) found: reject
is ' ' (space) found: accept


---

bug 1: it should search from the beginning (left end of tape) so that it doesnt miss a pair to the left.

bug2: I can do two phases and to create a sub-routine for each letter it encounters first, such as:
if found unmarked u: search for unmarked d
if found unmarked d: searc for unmarked u

and also for the (r,l) pair.

bug3: it is covered in the previous fix, as it searched for unmarked characters.

bug4: covered in 1.

bug 5: after all phases finished, search for an unmarked character, if not one found (found a space) then accept