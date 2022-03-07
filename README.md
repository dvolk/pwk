# PWK

PWK is a line processing program with a familiar Python syntax.

## Installation

    pip3 install argh
    wget https://raw.githubusercontent.com/dvolk/pwk/master/pwk
    sudo cp pwk /usr/bin
    sudo chmod 755 /usr/bin/pwk

## Running

PWK has 3 arguments, an if expression which filters the lines to process, a process expression, which modifies the lines, and a final lines expression, which operates on the filtered and processed lines as a whole (for eg. sorting).

See examples.

## Examples

### Print the top 10 most common 5 letter roots of american-english words

    cat /usr/share/dict/american-english | pwk \
        -p "line[0:5]" \
        -f "[f'root: {root}, occurences: {count}' for root, count in sorted(collections.Counter(lines).items(), key=lambda x: x[1], reverse=True)][0:10]"

Output:

    root: inter, occurences: 325
    root: under, occurences: 239
    root: trans, occurences: 234
    root: super, occurences: 131
    root: count, occurences: 120
    root: disco, occurences: 119
    root: contr, occurences: 103
    root: elect, occurences: 85
    root: overs, occurences: 84
    root: const, occurences: 77

### Print names of all html documents in a directory

    find ../../nim-1.6.2/ | pwk \
        -i 'line[-4:] == "html"' \
        -p "Path(line).stem" \
        -f "sorted(set(lines))"

Output:

    active
    algorithm
    aliases
    apis
    asciitables
    ...
