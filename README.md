import random
import string

def generate_password(username, email, length=12):
    if length < 6 or length > 32:
        raise ValueError('Password length must be between 6 and 32 characters.')
    
    char_set = '!#$%&()*+,-./:;<=>?@[\\]_`{|}~' + string.ascii_letters + string.digits
    while True:
        password = ''.join(random.choices(char_set, k=length))
        
        # Ensure at least one uppercase letter
        if not any(char.isupper() for char in password):
            continue
        
        # Check for consecutive identical characters
        if any(password[i] == password[i+1] == password[i+2] for i in range(len(password) - 2)):
            continue
        
        # Ensure it doesn't contain username or email
        if username in password or email in password:
            continue
        
        return password

# Example usage
username = 'sai'
email = 'sai@example.com'
password = generate_password(username, email, 12)
print(f'Generated Password: {password}')
