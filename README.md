PROJECT SUMMARY

# SECURE-DATA-TRANSFERS-WITH-ENCRYPTION
This project delves into hybrid encryption approach using AES for fast and secure data encryption, and RSA for protecting the encryption key. The system simulates secure data transmission, such as banking, health cares, election results, ensuring confidentiality, integrity, and reliability of the information during transfer.


<img width="669" height="252" alt="image" src="https://github.com/user-attachments/assets/eb19b2e7-8558-495a-83b5-71001c56b7f1" />



TITLE: SECURE DATA TRANSFERS WITH ENCRYPTION

AIM: To evaluate a hybrid encryption system using AES and RSA and ensure secure data transmission and confidentiality.

PROBLEM STATEMENT: In today’s digital world, large volumes of sensitive data are transmitted across computer networks. However, transmitting data over unsecured networks exposes it to risks such as interception, unauthorized access, and manipulation. This creates a need for secure mechanisms to protect data during transmission.

OBJECTIVE: 

	To enhance the security of data transmitted across networks.
	Demonstrates the use of hybrid encryption (AES and RSA) for secure communication.
	Enhance security using Initialization Vector (IV)

SCOPE OF THE STUDY:

	Implements secure data transfer using AES and RSA encryption techniques
	Demonstrates encryption, key exchange, and decryption processes.
	Uses a dataset to simulate secure data transmission and implement using python in a simulated environment.

DATA SOURCE:

The dataset used in this study was sourced from kaggle, a widely recognized platform for open datasets and machine learning resources. 
TOOLS & TECHNOLOGY
The implementation was carried out using the following technologies:
•	Python programming language 
•	PyCryptodome for cryptographic operations 
•	pandas for dataset handling 
•	Google Colab for development and execution 

DATA PREPROCESSING

The dataset, titled Data_for_Security and Communication.csv, was imported into the computational environment using Google Colab file upload functionality. The dataset was loaded into a structured DataFrame using the pandas’ library for efficient data manipulation and analysis. To ensure compatibility with cryptographic processes, the dataset was converted into JavaScript Object Notation (JSON) format, providing a standardized structure. The JSON data was then encoded into byte format, as cryptographic algorithms operate on binary data.



Tools and Libraries Used

The implementation was carried out using the following technologies:
•	Python programming language 
•	PyCryptodome for cryptographic operations 
•	pandas for dataset handling 
•	Google Colab for development and execution 

METHODOLOGY

The dataset used in this study was sourced from kaggle, a widely recognized platform for open datasets and machine learning resources. The dataset, titled Data_for_Security and Communication.csv, was imported into the computational environment using Google Colab file upload functionality.
The dataset was loaded into a structured DataFrame using the pandas library for efficient data manipulation and analysis. To ensure compatibility with cryptographic processes, the dataset was converted into JavaScript Object Notation (JSON) format, providing a standardized structure. The JSON data was then encoded into byte format, as cryptographic algorithms operate on binary data.

Symmetric Encryption Using AES
To ensure efficient and secure data encryption, the AES (Advanced Encryption Standard) algorithm was implemented in Cipher Block Chaining (CBC) mode.


AES key pair Generation

A 128-bit symmetric encryption key was generated using a cryptographically secure random function:
•	get_random_bytes (16) 
This method ensures the randomness and unpredictability of the encryption key, thereby enhancing resistance to brute-force attacks.
Asymmetric Encryption Using RSA
To securely transmit the AES key, the RSA (Rivest–Shamir–Adleman) algorithm was utilized

RSA key pair Generation

A 2048-bit RSA key pair was generated, consisting of:
•	A private key, which is securely maintained
•	A public key, which is shared for encryption purposes
Key Decryption at Receiver End
Upon receiving the encrypted data, the first step for the receiver is to recover the AES encrypted key.


Process:
1.	The receiver uses the RSA private key to decrypt the encrypted AES key.
2.	The original AES key is restored.
Since the private key is only accessible to the receiver, unauthorized users cannot retrieve the encryption key.
Data Integrity Verification
 To confirm that the data was not altered during transmission, a verification step is performed. The decryption dataset is compared with the original dataset using validation techniques. If both datasets match, the system confirms that:
•	The encryption process worked correctly
•	No data corruption occurred during transmission.

##Key Insights from the Project: Secure Data Transfers with Encryption##

 Effectiveness of Hybrid Encryption
The combination of Advanced Encryption Standard and RSA algorithm demonstrates a strong and practical approach to secure data transmission.

AES provides fast and efficient encryption for large datasets
RSA ensures secure key exchange, solving the key distribution problem
This hybrid approach leverages the strengths of both algorithms, making it suitable for real-world applications such as secure web communication and online transactions.

 


CONCLUSION
 Secure Data Transfers with Encryption play a pivotal role in protecting sensitive information, ensuring data confidentiality, integrity, and availability. This study develops a secure hybrid model by pairing AES's efficiency with RSA's strong key management. By incorporating an Initialization Vector, the framework removes predictable patterns in the encrypted data, ensuring higher levels of confidentiality during transfer. future research should investigate advanced key management frameworks, such as: Key rotation mechanisms, Secure key storage (e.g., hardware security modules), Distributed key management systems.

 
# STEP 1: Load Dataset
df = pd.read_csv("Data_for_Security and Communication.csv")
# Convert dataset to JSON string
data_json = df.to_json()
data_bytes = data_json.encode()
# Install library
!pip install pycryptodome

from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes
from Crypto.Util.Padding import pad

 STEP 2: AES Encryption
 
# Generate AES key
aes_key = get_random_bytes(16)  # 128-bit key

# Create AES cipher (CBC mode)
cipher_aes = AES.new(aes_key, AES.MODE_CBC)

# Encrypt data (must be bytes and padded)
ciphertext = cipher_aes.encrypt(pad(data_bytes, AES.block_size))

# Get initialization vector (IV)
iv = cipher_aes.iv

print("AES Key:", aes_key)
print("IV:", iv)
print("Ciphertext:", ciphertext[:50])
AES Key: b'\xb8\xbe\xfb\x14\xda\xf3\xbd\x84\xf1\x81P\xee\xef\xbeX8'
IV: b'\xd9V\xef\x16\x02\x12g\xd2\xf7\x85\xcb2\xd7\xc9p\x96'
Ciphertext: b'\x01.\x96\x11\x88\xe2]&\xdd\xb8\x96\xbb\x97k\xa6\xf4\xc7\x99\xd4\x96GG\xde6\xa5\x86IdU\xc6n\x1d\x80\x8e<\x7f\xeaB\xc3\x106C6MW\xdd\x88\x9f\xf1>'

# STEP 3: RSA Key Generation

# Generate RSA key pair
key = RSA.generate(2048)

# Extract public key
public_key = key.publickey()

# Encrypt AES key using RSA public key
cipher_rsa = PKCS1_OAEP.new(public_key)
encrypted_aes_key = cipher_rsa.encrypt(aes_key)

print("Public Key:\n", public_key.export_key())
print("Encrypted AES Key:\n", encrypted_aes_key[:50])
Public Key:
 b'-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAuutnH8N/3aJ99anb1Se1\n5loTKfHseLOiVD6TBM6qmQbFNcr6QzxfNIxkiL++fyiiu9EJwXRZ8synE5oaJEua\nhPTsdQI86C6qnBxYh5BojNJ58NFRpRfTHN+yFnWaLOnT8qS7KqTtgn/DJ5HHahkX\nY+uT0yAV2Cfreb1f5zDshugDWBosqaQr+kDoF236hRNR67fxQ9AntLM9JiriAfth\nliFCbT0EUFVq5DNNuC2CzqPYdR6NXePrf1B0nBlP+WdoFAevwbc+pzu8xMb47nZC\nwdu2xGxIilDaDlSxThB6Ietlb6qEfozhWh656/AxPtNfeu67lVQOx1agfd6PeU1/\newIDAQAB\n-----END PUBLIC KEY-----'
Encrypted AES Key:
 b'\x9b\x16\xcd\x8a\x94\x14\x1b\x81\xb9\x04\xcb\xa1\xae\xc9A\x9c\xbew\xbd\xcby\x05\xfb,\xb6\x9f4\xfd\xab<\x97 C\x1c<g\xe3\xd3\xda{\xc7\xf7P\x01\xddN\x9c:\xc4\xd6'


 
# STEP 4: RSA Decryption

encrypted_key_bytes = base64.b64decode(transmitted_data["encrypted_key"])

cipher_rsa_dec = PKCS1_OAEP.new(key)
decrypted_aes_key = cipher_rsa_dec.decrypt(encrypted_key_bytes)

print("Decrypted AES Key:", decrypted_aes_key)
Decrypted AES Key: b'\xb8\xbe\xfb\x14\xda\xf3\xbd\x84\xf1\x81P\xee\xef\xbeX8'
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad
import base64
 
 
 # STEP 5: AES Decryption

iv = base64.b64decode(transmitted_data["iv"])
ciphertext = base64.b64decode(transmitted_data["ciphertext"])

cipher_aes_dec = AES.new(decrypted_aes_key, AES.MODE_CBC, iv=iv)

decrypted_data = unpad(cipher_aes_dec.decrypt(ciphertext), AES.block_size)

decrypted_json = decrypted_data.decode()

print("Decryption Successful:", decrypted_json == data_json)
Decryption Successful: True


from cryptography.fernet import Fernet

# Step 1: Generate Key
key = Fernet.generate_key()
cipher = Fernet(key)

# Step 2: Sender encrypts message
message = b"Hello, this is a secure message"
encrypted_message = cipher.encrypt(message)

print("Encrypted:", encrypted_message)

# Step 3: Receiver decrypts message
decrypted_message = cipher.decrypt(encrypted_message)

print("Decrypted:", decrypted_message.decode())
Encrypted: b'gAAAAABp8QmfVu-4Pb_54M5yTiwt5pNgR0bMrLSSN8hvRR9zMRWDG_MjtaocyV8JQT0jWMgLuYbjuvhPRmkoGOIjr5fXSTDKAint1-KWPtFQ7vDwoLA1BoI='
Decrypted: Hello, this is a secure message

Prototype Diagram

[Sender] │ ▼ [Encryption] │ ▼ [Encrypted Data] →→→ (Network) →→→ │ ▼ [Decryption] │ ▼ [Receiver]



