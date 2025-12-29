# A high-performance password strength validator using Entropy calculation
import math
import re

def calculate_entropy(password):
    """Calculates the bits of entropy for a given password."""
    if not password:
        return 0
    charset = 0
    if re.search(r'[a-z]', password): charset += 26
    if re.search(r'[A-Z]', password): charset += 26
    if re.search(r'[0-9]', password): charset += 10
    if re.search(r'[^a-zA-Z0-9]', password): charset += 32
    
    entropy = len(password) * math.log2(charset)
    return round(entropy, 2)

def validate_password(password):
    entropy = calculate_entropy(password)
    strength = "Weak"
    if entropy > 60: strength = "Strong"
    elif entropy > 40: strength = "Medium"
    
    return {"password": password, "entropy_bits": entropy, "strength": strength}

# Example usage
print(validate_password("P@ssw0rd123!"))
