import re
import pandas as pd

chat_file = "D:\ACADEMIA\Research\Yerusa\WhatsApp Chat with KYC.txt"

def analyze_whatsapp_chat(chat_file):
    """Analyzes a WhatsApp group chat exported as a .txt file."""

    events = []
    with open(chat_file, 'r', encoding='utf-8') as f:
        for line in f:
            # Check for group creation event
            match = re.search(r'(\d+/\d+/\d+), (\d+:\d+) - (.*) created group "(.*)"', line)
            if match:
                date, time, creator, group_name = match.groups()
                events.append({
                    'Date': date,
                    'Time': time,
                    'Event': 'Group Created',
                    'Member': creator,
                    'Group Name': group_name
                })

            # Check for member added events 
            match = re.search(r'(\d+/\d+/\d+), (\d+:\d+) - (.*) added (.*)', line)
            if match:
                date, time, adder, added_member = match.groups()
                events.append({
                    'Date': date,
                    'Time': time,
                    'Event': 'Member Added',
                    'Member': added_member,
                    'Added by': adder
                })

            # Check for members leaving (both user-initiated and system messages)
            match_left = re.search(r'(\d+/\d+/\d+), (\d+:\d+) - (.*) left', line)
            match_system = re.search(r'(\d+/\d+/\d+), (\d+:\d+) - System: (.*) left', line)
            if match_left or match_system:
                date, time, member = match_left.groups() if match_left else match_system.groups()
                events.append({  # Create a new event
                    'Date': date,
                    'Time': time,
                    'Event': 'Member Left',
                    'Member': member
                })

    return pd.DataFrame(events)

# Example usage
chat_file = "D:\ACADEMIA\Research\Yerusa\WhatsApp Chat with KYC.txt"  # Replace with your chat file path
df = analyze_whatsapp_chat(chat_file)

# Display the resulting DataFrame
print(df)

# Save results to a CSV file (optional)
df.to_csv('KYC_one.csv', index=False) 
