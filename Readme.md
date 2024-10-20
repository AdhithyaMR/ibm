## import the requests
```py
import requests
```
## Code for app.py
```py
import requests

def add_food_item(description, quantity, pickup_location, pickup_instructions=None, contact_info=None):
    try:
        response = requests.post('http://localhost:5001/add_food', json={
            "description": description,
            "quantity": quantity,
            "pickup_location": pickup_location,
            "pickup_instructions": pickup_instructions,
            "contact_info": contact_info
        })
        response.raise_for_status()  # Check for HTTP errors
        return response.json()  # Return the response data
    except requests.exceptions.RequestException as e:
        return {"error": str(e)}  # Return the error message

def get_available_food():
    try:
        response = requests.get('http://localhost:5001/food')
        response.raise_for_status()  # Check for HTTP errors
        return response.json()  # Return the response data
    except requests.exceptions.RequestException as e:
        return {"error": str(e)}  # Return the error message

def main():
    print("Welcome to the Food Donation App!")
    while True:
        print("\n1. Add Food Item")
        print("2. Get Available Food Items")
        print("3. Exit")
        choice = input("Choose an option (1/2/3): ")

        if choice == '1':
            description = input("Enter food description: ")
            quantity = input("Enter quantity: ")
            pickup_location = input("Enter pickup location: ")
            pickup_instructions = input("Enter pickup instructions (optional): ")
            contact_info = input("Enter contact info (optional): ")
            
            response = add_food_item(description, quantity, pickup_location, pickup_instructions, contact_info)
            print("Response:", response)

        elif choice == '2':
            available_food = get_available_food()
            if "error" in available_food:
                print("Error retrieving food items:", available_food["error"])
            else:
                print("Available Food Items:")
                for item in available_food:
                    print(f"Description: {item['description']}, Quantity: {item['quantity']}, Pickup Location: {item['pickup_location']}")

        elif choice == '3':
            print("Exiting the app. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

# Uncomment the next line to run the app when the cell is executed
# main()
```
## Run the file
```py
# Uncomment the next line to run the app when the cell is executed
main()
```
