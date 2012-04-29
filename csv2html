#!/usr/bin/env python

import csv
import itertools
import string
import sys

input = sys.stdin
start_lines = input.readlines(10)
all_input = itertools.chain(iter(start_lines), input)

def detect_delimiter(iterable, char_set):
    matches = (c for c in char_set if c in iterable)
    return next(matches, None)

def detect_csv_dialect(sample):
    try:
        return csv.Sniffer().sniff(sample)
    except:
        return None

delimiter = detect_delimiter(start_lines[0], list('\t, '))
reader = None

if delimiter in list('\t,'):
    # try to detect csv dialect, which should neatly handle quoted separators and stuff
    dialect = detect_csv_dialect(''.join(start_lines))
    if dialect:
        reader = csv.reader(all_input, dialect)

if not reader:
    if delimiter in list(string.whitespace):
        # use str.split() with no arguments to split on arbitrary whitespace strings
        reader = (line.strip().split() for line in all_input)
    else:
        reader = all_input

print "<TABLE>"
for row in reader:
    print "  <TR>"
    print "    <TD>" + "</TD><TD>".join(row) + "</TD>"
    print "  </TR>"
print "</TABLE>"
