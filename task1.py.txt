import random
import string

# Define lists of adjectives and nouns
adjectives = ["Cool", "Happy", "Silly", "Brave", "Clever", "Swift", "Fierce", "Charming", "Witty", "Bright"]
nouns = ["Tiger", "Dragon", "Panda", "Fox", "Eagle", "Shark", "Wolf", "Bear", "Lion", "Hawk"]

# Generate a random username
def generate_username(include_number=True, include_special=False, length=8):
    adj = random.choice(adjectives)
    noun = random.choice(nouns)
    username = adj + noun

    # Add a number if requested
    if include_number:
        number = str(random.randint(0, 999))
        username += number

    # Add a special character if requested
    if include_special:
        special_char = random.choice(string.punctuation)
        username += special_char

    # Ensure the length matches the desired value
    if len(username) > length:
        username = username[:length]

    return username

# Save usernames to a file
def save_usernames(usernames, filename="usernames.txt"):
    with open(filename, "w") as file:
        for username in usernames:
            file.write(username + "\n")

# Get user preferences
def get_user_preferences():
    include_number = input("Include numbers? (yes/no): ").lower() == "yes"
    include_special = input("Include special characters? (yes/no): ").lower() == "yes"
    length = int(input("Enter desired length of username (minimum 6, max 20): "))
    length = max(6, min(length, 20))
    return include_number, include_special, length

# Main function
def main():
    num_usernames = int(input("How many usernames would you like to generate? "))
    include_number, include_special, length = get_user_preferences()
    
    usernames = [generate_username(include_number, include_special, length) for _ in range(num_usernames)]

    # Display generated usernames
    print("\nGenerated Usernames:")
    for username in usernames:
        print(username)

    # Save usernames to file
    save_usernames(usernames)
    print(f"\nUsernames saved to usernames.txt")

if __name__ == "__main__":
    main()
