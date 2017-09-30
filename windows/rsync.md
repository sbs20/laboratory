# Rsync

The short version is: ultimately you need cygwin. However,
[DeltaCopy](http://www.aboutmyip.com/AboutMyXApp/DeltaCopy.jsp) offers a 
nice, easy Windows UI wrapper and includes the core cygwin libraries and
rsync.exe. The problem is that the rsync and cygwin libraries date from around
2008; they don't support long filenames or unicode files.

It turns out, though, that there are some hints on the website for
[supporting unicode](http://www.aboutmyip.com/AboutMyXApp/DisplayFAQ.do?fid=23) and
[using up to date files](http://www.aboutmyip.com/AboutMyXApp/DisplayFAQ.do?fid=12).

To work around these problems:

  1. [Download Cygwin](https://cygwin.com/)
  1. Run the cygwin install
  1. Choose "Download without installing" and then a download location
  1. Navigate into the file hierarchy for
      * x86_64
          * release
              * cygwin = cygwin1.dll
              * libiconv = cygiconv-2.dll
              * openssh = ssh.exe
              * rsync = rsync.exe
     You will need to look through some tar.gz archives for the right files

Once you have these, you can copy them into your DeltaCopy directory and hey presto!
