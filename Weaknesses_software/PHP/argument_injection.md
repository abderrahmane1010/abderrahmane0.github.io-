# CWE-88: Improper Neutralization of Argument Delimiters in a Command ('Argument Injection')

* Description :

  The product constructs a string for a command to be executed by a  separate component in another control sphere, but it does not properly  delimit the intended arguments, options, or switches within that command string. 

* Consequences :

  An attacker could include arguments that allow unintended commands or  code to be executed, allow sensitive data to be read or modified or  could cause other unintended behavior. 



