import random
import string

def check_password_strength(password):
    score = 0
    feedback = []
    
    # 1. Length check
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("❌ Password should be at least 8 characters long.")
        
    # 2. Uppercase check
    if any(c.isupper() for c in password):
        score += 1
    else:
        feedback.append("❌ Must contain at least one uppercase letter (A-Z).")
        
    # 3. Lowercase check
    if any(c.islower() for c in password):
        score += 1
    else:
        feedback.append("❌ Must contain at least one lowercase letter (a-z).")
        
    # 4. Digit check
    if any(c.isdigit() for c in password):
        score += 1
    else:
        feedback.append("❌ Must contain at least one number (0-9).")
        
    # 5. Special character check
    special_chars = "!@#$%^&*()_+-=[]{}|;:,.<>?"
    if any(c in special_chars for c in password):
        score += 1
    else:
        feedback.append("❌ Must contain at least one special character (!@#$...).")
        
    # Evaluate result
    print("\n--- Password Analysis Report ---")
    if score == 5:
        return "🟢 **Strong:** Excellent! This is a very secure password."
    elif score >= 3:
        return "🟡 **Medium:** Good, but consider adding the following to make it stronger:\n" + "\n".join(feedback)
    else:
        return "🔴 **Weak:** This password is too weak! Fix the following issues:\n" + "\n".join(feedback)

def generate_strong_password():
    # Automatically generate a strong password
    length = 12
    chars = string.ascii_letters + string.digits + "!@#$%^&*"
    password = "".join(random.choice(chars) for _ in range(length))
    return password

# Main Program
if __name__ == "__main__":
    print("--- Welcome to Password Security Tool ---")
    user_pass = input("Enter the password you want to check: ")
    print(check_password_strength(user_pass))
    
    print("\n----------------------------------------")
    choice = input("Do you want me to generate a strong password for you? (yes/no): ").lower()
    if choice == 'yes':
        print(f"✨ Generated Strong Password: **{generate_strong_password()}**")
