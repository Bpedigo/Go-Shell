The overall goal of this program is to make commonly done task at the command line easier.  If you’re like me you probably have a whole bunch of tiny batch files that make certain tasks faster. For example, if you’re working on the on the same file over and over again you could easily create a batch file to open that file. An example:
=================================
@echo off
Start winword “C:\path\to\doc.doc”
================================

You could save the above code in a file named doc.bat and add it to a directory that is used in the environment variables and now when you type doc on the command line the file opens.  But I thought why not do the same thing but with PowerShell.  So I came up with this program. It’s a power shell module so you can add it in easily.  Once the module is loaded you can start using the new command. There are three major commands open, goto, bir.
