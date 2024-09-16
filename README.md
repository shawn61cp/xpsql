# xpsql
Bash script to automate startup of PSQL and PSPG connected via a named pipe under TMUX

## Introduction
There exists a wonderful pager [PSPG](https://github.com/okbob/pspg) developed for PostgreSQL.  It is useful for other things as well.

One of its fantastic features is the ability to continuously read input from a named pipe.  So, if you direct the query output from PSQL to this pipe, you have the ability to see your data and work with queries etc at the same time.

I like TMUX for text windowing and so I wrote this script to automate the creation of a pane for data display, starting PSPG in this pane, starting PSQL in the original pane, and setting both up for communication via a named pipe.

## Prerequisites
* Packages needed for your distribution
  * postgresql-client
  * pspg
  * tmux
 
## Installation
- Download the <code>xpsql</code> script from this repository to a location of your choice, preferably somewhere along your <code>PATH</code>.  This example will use <code>/$HOME/.local/bin</code> but you could install it system-wide by placing it for instance in <code>/usr/local/bin</code>.
- Create two symlinks to the script in the same location.
  - <code>cd $HOME/.local/bin</code>
  - <code>ln -s xpsql xpsqlv</code>
  - <code>ln -s xpsql xpsqlh</code>
- In your home directory create the named pipe.  If you have installed this system-wide, any user who uses the script will need to do this step (only once).
  - <code>cd $HOME</code>
  - <code>mkfifo psql1</code>

## Usage
Enter <code>xpsql -h</code> for usage/help.

Run <code>xpsqlv</code> (in a TMUX window) to produce panes that are vertically stacked. Run <code>xpsqlh</code> to produce panes that are placed horizontally side-by-side.  <code>xpsql</code> by itself defaults to vertical stacking.

In both cases follow the command with arguments just as you would for PSQL.  When you exit PSQL, the created pane along with the PSPG instance will be destroyed.

NOTE: PSPG will appear unresposive until the first time some output is sent from PSQL.
