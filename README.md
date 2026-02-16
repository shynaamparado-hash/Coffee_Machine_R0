# Coffee_Machine_R0

This is a Python-based coffee_machine simulation project.
Features:
- Resource tracking
- Coin processing
- Menu system

        MENU = {
            "espresso": {
                "ingredients": {
                    "water": 50,
                    "coffee": 18,
                },
                "cost": 1.5,
            },
            "latte": {
                "ingredients": {
                    "water": 200,
                    "milk": 150,
                    "coffee": 24,
                },
                "cost": 2.5,
            },
            "cappuccino": {
                "ingredients": {
                    "water": 250,
                    "milk": 100,
                    "coffee": 24,
                },
                "cost": 3.0,
            }
        }
        
        resources = {
            "water": 500,
            "milk": 200,
            "coffee": 100}
        profit = 0
        
        def make_coffee():
            query = input("What would you like?").lower()
        
            def subtract_resources(coffee_ing):
                for item in MENU[coffee_ing]["ingredients"]:
                    resources[item] -= MENU[coffee_ing]["ingredients"][item]
        
            def process_coins(money):
                global profit
        
                if money == MENU[query]["cost"]:
                    profit += MENU[query]["cost"]
                    print(f"Here's your {query}☕, enjoy!")
                    subtract_resources(query)
        
                elif money > MENU[query]["cost"]:
                    profit += MENU[query]["cost"]
                    change = money - MENU[query]["cost"]
                    print(f"Here's your {query}☕, enjoy!")
                    print(f"Your total money is {money}. Here's your change ₱{change}.")
                    subtract_resources(query)
        
                else:
                    print(f"Sorry that's not enough money. Money ₱{money} refunded.")
        
            def insert_coin():
                print("Please insert coin.")
                centavos_25 = int(input("How many centavos '₱ 0.25': "))
                peso = int(input("How many peso '₱1.00': "))
                singko = int(input("How many singko '₱5.00': "))
                gis = int(input("How many gis '₱10.00': "))
                payment = (centavos_25 * 0.25) + (peso * 1.00) + (singko * 5.00) + (gis * 10.00)
        
                process_coins(payment)
        
            def check_resources(coffee):
                for item in MENU[coffee]["ingredients"]:
                    if MENU[coffee]["ingredients"][item] > resources[item]:
                        print(f"Sorry there is not enough {item}.")
                        return
        
                insert_coin()
        
            def command_coffee_machine(command):
                if command == "off":
                    global coffee_machine_on
        
                    print("...Turning off...")
                    coffee_machine_on = False
        
                elif command == "report":
                    for key, value in resources.items():
                        print(f"{key}: {value}")
        
                elif command in MENU:
                    check_resources(command)
        
                elif command == "profit":
                    print(f"Your total profit is ₱{profit}")
        
            command_coffee_machine(query)
        
        
        
        coffee_machine_on = True
        
        while coffee_machine_on:
            make_coffee()
