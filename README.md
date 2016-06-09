`argv` is a tiny C program that just prints its arguments,
one per line.
It is sometimes handy when you're debugging
shell commands that run commands, for instance:

argv a "b c"
sudo argv a "b c"
ssh foo argv a "b c"
ssh foo argv a \"b c\"
ssh foo sudo argv a \"b c\"

I was inspired to write `argv` by reading
[this StackOverflow question](http://stackoverflow.com/questions/37660229/shell-parallel-command-to-execute-as-user-postgres-via-root/37731999)
about how this command acted differently
on newer vs older machines:

    parallel -q -j0 ssh {} -l root "sudo -u postgres  -i psql -tAc
        \"select current_user, current_database()\" -d \$(echo {}| cut -d@ -f1) "
        ::: db_foo@host1 db_bar@host2 ...


Getting started
---------------

First do this:

    autoreconf --install

Then to build, just:

    ./configure
    make
    sudo make install


