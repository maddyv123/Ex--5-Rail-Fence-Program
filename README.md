# Ex--5-Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
def encrypt_rail_fence(text, rails):
    rail = [['\n' for _ in range(len(text))] for _ in range(rails)]
    
    # Create the Rail Fence pattern
    row, down = 0, False
    for i, char in enumerate(text):
        rail[row][i] = char
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1
    
    # Read the encrypted text in row-wise order
    cipher = []
    for r in rail:
        cipher.extend([c for c in r if c != '\n'])
    
    return "".join(cipher)

def decrypt_rail_fence(cipher, rails):
    rail = [['\n' for _ in range(len(cipher))] for _ in range(rails)]
    
    # Mark positions to fill
    row, down = 0, False
    for i in range(len(cipher)):
        rail[row][i] = '*'
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1
    
    # Place characters in the rail matrix
    index = 0
    for r in range(rails):
        for c in range(len(cipher)):
            if rail[r][c] == '*' and index < len(cipher):
                rail[r][c] = cipher[index]
                index += 1
    
    # Read the text in a zigzag manner
    result = []
    row, down = 0, False
    for i in range(len(cipher)):
        result.append(rail[row][i])
        if row == 0 or row == rails - 1:
            down = not down
        row += 1 if down else -1
    
    return "".join(result)

# Get user input
plain_text = input("Enter the text to encrypt: ")
rails = int(input("Enter the number of rails: "))

# Encrypt and decrypt
encrypted_text = encrypt_rail_fence(plain_text, rails)
print("\nEncrypted:", encrypted_text)

decrypted_text = decrypt_rail_fence(encrypted_text, rails)
print("Decrypted:", decrypted_text)


# OUTPUT
![Screenshot 2025-03-27 091852](https://github.com/user-attachments/assets/f01ddac7-0b27-483d-8aac-de18328d56bf)

# RESULT
The code executed successfully!
