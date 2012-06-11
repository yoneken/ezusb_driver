ezusb_driver
============

This is a Cypress EZ-USB Windows driver for Windows Vista/7(x64).
Since Windows Vista x64, We cannot install non digitally signed driver.


[How to install]

1. Install cyusb.pfx.
	Click 'Next', 'Next' ...
	Password: oreore

2. Run command prompt as administrator.

3. Type 'bcdedit /set TESTSIGNING ON'.

4. Restart your computer.

5. Connect your EZ-USB to your computer.
	Automatically installer will fail.

6. Install the driver manually.
	At device manager.
	Choose this directory.


[How to make a signed driver]

Actually, if you have installed Microsoft Visual Studio (or Windows SDK), you can sign any driver you want.

1. Get SuiteUSB from Cypress web page (http://www.cypress.com/?rID=34870).

2. Install SuiteUSB.

3. Run Windows SDK command shell as administrator.
	In start menu.

4. Change directory to C:\Cypress\Cypress Suite USB 3.4.7\Driver\bin\wlh\x64.
	There are cyusb.sys and cyusb.inf.

5. Type 'makecert -sv cyusb.pvk -a sha1 -r -ss YOURPASSWORD -len 1024 -sr localmachine -$ individual -n CN="cyusb.sys" cyusb.cer'.
	Change YOURPASSWORD you want.
	Remember your password and secret key.

6. Type 'cert2spc cyusb.cer cyusb.spc'.

7. Type 'pvk2pfx -pvk cyusb.pvk -pi YOURPASSWORD -spc cyusb.spc -pfx cyusb.pfx -po YOURPASSWORD'.

8. Type 'signtool sign /f cyusb.pfx /p YOURPASSWORD  /d "cyusb.sys" /v cyusb.sys'.

Then, you get cyusb.cer, cyusb.pfx, cyusb.pvk and cyusb.spc.
Let's start to install the driver.

