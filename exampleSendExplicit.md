### Definition: sendExplicit
+ Description: Format by which tokens are transferred to one or more recipients. Any token change returned to change output.
+ Structure:
	* tokenOut [flags] [tokenOut] [tokenOut] [...] [tokenOut]
+ Flags:
	* 0: Set if tokenID is specified for all following tokenOut structures. Clear for all following tokenOut structures to inherit tokenID of first tokenOut structure.
	* 1: Set if indexOut is specified for all following tokenOut structures. Clear will increment sequentially for all following tokenOut structures, starting from indexOut of first tokenOut structure.
	* 2 - 7: Reserved
+ Dependencies:
	* Structure: tokenOut

### Structure: tokenOut
+ Description: Structure used in explicit sends
+ Elements:
	* tokenID
	* indexOut
	* quantity(n)

### Construct: quantity
+ Description: A representation of quantity for which the value depends on the properties of a given transaction.
+ Condition: When value of output at indexOut is equal to dust, n is of type 64-bit unsigned integer, and quantity is equal to value of n. When value of output at indexOut is greater than dust, n is of type 8-bit unsigned integer, and quantity is equal to (value - dust) * 10 ** n
+ Size: 8-bit unsigned integer, 1 byte or 64-bit unsigned integer, 8 bytes
+ Valid values: 0 to 255 or  1 to 9,223,372,036,854,775,807

### Constant: dust
+ Description: A quantity of atomic units of Bitcoin which represents the smallest standard output
+ Size: 16-bit unsigned integer
+ Valid values: 0 to 65535
+ Value: 5460

### sendExplicit size analysis
+ Single recipient
	* Size: 6 bytes minimum, 13 bytes maximum
+ Multiple recipients
	* Overhead: 7 bytes minimum, 14 bytes maximum
	* Size for added recipients: 1 byte minimum, 13 bytes maximum
+ Potential recipients in a single transaction given 40 bytes of data:
	* 34 unique recipients.