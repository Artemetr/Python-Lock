from math import floor, ceil, fabs
from threading import Thread, Lock
from time import sleep
from os import system
import sys

l1 = Lock()
l2 = Lock()
stop_thread = False
work_with = [0, 1, 1]

def input_arg(count=3):
	i = 0
	arguments = []
	while True:
		temp = input('Input var' + str(i + 1) + ': ')
		try:
			if i == 2 and float(temp) <= 0:
				print("Step can not be less then zero, repeat input\n")
				continue
		except ValueError:
			print('Invalid variable type, try again\n')
			continue
		try:
			temp = float(temp)
		except ValueError:
			print('Invalid variable type, try again\n')
			del temp
			continue
		else:
			arguments.append(temp)
		if i == count - 1:
			break
		else:
			i += 1
	return arguments
def sum_of():
	while True:
		l1.acquire()
		if stop_thread is True:
			break

		low, up, step = work_with[0], work_with[1], work_with[2]
		if low > up:
			temp = up
			up = low
			low = temp
		res = low
		stcount = int((up - low) / step)
		for i in range(stcount):
			res += low + step * (i + 1)
		
		print(f"Sum of arange is: {res}")
		l1.release()
		sleep(4)

def pow_of():
	while True:
		l2.acquire()
		if stop_thread is True:
			break

		low, up, step = work_with[0], work_with[1], work_with[2]
		if low > up:
			temp = up
			up = low
			low = temp
		res = low
		stcount = int(fabs(up - low) / step)
		for i in range(stcount):
			res *= low + step * (i + 1)

		print(f"Power of arange is: {res}")
		l2.release()
		sleep(4)

def submenu():
	while True:
		cmd = input("\nDo you wanna leave? y/n : yes/no\n")
		if cmd == 'y':
			return True
		else:
			return False

thsum = Thread(target=sum_of)
thpow = Thread(target=pow_of)
l1.acquire()
l2.acquire()

thsum.start()
thpow.start()

msg = "\nCommand list: q - quit; i - input three variable; t - start threads;"
msg_arg = "Arguments now is "
while True:
	system('cls')
	print(msg)
	print(msg_arg, work_with)
	cmd = input()
	if cmd is 'q':
		if submenu():
			stop_thread = True
			l1.release()
			l2.release()
			break
	elif cmd is 'i':
		print("Enter low, upper borders and step which can't be a zero:\n")
		work_with = input_arg(3)
	elif cmd is 't':
		l1.release()
		l2.release()
		sleep(3)
		l1.acquire()
		l2.acquire()
	else:
		print("Unknown command, please try an input again.\n")
		sleep(3)
