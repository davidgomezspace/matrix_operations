PURPOSE

This program is a bash shell script that utilizes bash builtins and Unix utilities to calculate basic matrix operations using input from either a file or stdin. The input format will be whole number values separated by tabs into a rectangular matrix. The script prints the dimensions of a matrix, transposes a matrix, calculates the mean vector of a matrix, adds two matrices, and multiplies two matrices.


REQUIREMENTS

	- bash shell (version 5.1.12 was used to develop the matrix script)
	- if using matrix textfiles, the files must be in the same directory as the matrix executable file


MAKE-EXECUTABLE

Make the matrix file executable by typing:
	$ chmod +x matrix


COMMANDS

	dims [MATRIX]
		- prints the the dimensions of the matrix as the number of rows followed by a space, then the number
		  of columns

	transpose [MATRIX]
		- reflects the elements of the matrix along the diagonal so an MxN matrix becomes an NxM matrix and
		  values along the diagonal will remain unchanged

	mean [MATRIX]
		- takes an MxN matrix and returns an 1xN row vector where the first element is the mean of column
		  one, the second element is the mean of column two, and so on

	add [MATRIX_LEFT] [MATRIX_RIGHT]
		- adds two matrices together element-wise to produce an MxN matrix, or returns an error if the
		  matrices do not have the same dimensions

	multiply [MATRIX_LEFT] [MATRIX_RIGHT]
		- multiplies an MxN and NxP matrix to produce an MxP matrix. Note: the operation is not cumulative
		  so A*B != B*A


EXAMPLES

Input matrices are contained in a text file or provided by the user through stdin. Example commands with
corresponding outputs, where $ represents the shell prompt and the user provides input files called matrix1.txt and matrix2.txt :

	$ cat matrix1.txt
	1	2	3	4
	5	6	7	8

	$ cat -et matrix1.txt    # The '-et' flag shows tabs as '^I' and newlines as '$', although check MAN pages for any changes to these flags
	1^I2^I3^I4$
	5^I6^I7^I8$

	$ cat matrix2.txt
	1	2
	3	4
	5	6
	7	8

	$ ./matrix dims matrix1.txt
	2	4

	$ cat matrix2.txt | ./matrix dims
	4	2

	$ ./matrix add matrix1.txt matrix1.txt
	2	4	6	8
	10	12	14	16

	$ ./matrix add matrix2.txt matrix2.txt
	2	4
	6	8
	10	12
	14	16

	$ ./matrix mean matrix1.txt
	3	4	5	6

	$ ./matrix transpose matrix1.txt
	1	5
	2	6
	3	7
	4	8

	$ ./matrix multiply matrix1.txt matrix2.txt
	50	60
	114	140


ERROR CHECKING

This program checks for the right number and format of arguments to the matrix.  This means it checks
that a given input file is readable before attempting to read it.  A valid matrix is a tab-delimited table
containing at least one element, where each element is a signed integer, every entry is defined, and the
table is rectangular. The following are examples of invalid matrices and will not be error-checked:
	- an empty matrix
	- a matrix where the final entry on a row is followed by a tab character
	- a matrix with empty lines
	- a matrix with any element that is blank or not an integer


NOTES

This program creates temporary files in your current directory and also removes them once the
program finishes calculating the output matrix


AUTHOR

David Gomez on January 29, 2018



