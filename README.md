# Pool Routes

### This is a simple code, storing pool route information, allowing the user to store and locate all pool route information they might need. (There are few variables stored for each route, this is mostly just a proof of concept). 

### How To Use: The code starts by giving a prompt, if you would like to add, delete or view the routes. you enter either a, d, or v to choose your option, any other input prints "Invalid input" and resends the original prompt. If you choose to add a route, it will prompt you for variables such as employee first name (the employee in charge of the route on a daily basis), employee last name, and route number. Variables could be added or deleted based on the user's needs. after entering the information, it will create a file, and store the route information as a list. Should you choose to delete a route for whatever reason (getting rid of the route, employee leave, etc...), the program will return a list of every route that is already stored, and it will assign each route a number (1-n routes). all the user has to do is select the number of the route they want to delete, and it will be permanently removed from the list. after each round of adding or deleting a route, the original prompt will show up again so the user can add, delete, or view the finalized list. finally if they are done editing the list, they can press v to view all routes. this returns all the routes as well as multiple variables such as payroll, total expenses, and total income. 

```python
t_cost_goods = 0
t_payroll = 0
other = 0
t_income = 0
net_profit = 0
t_expenses = 0

while True:
    x = input("\n\nAdd a route (a), Delete a current route(d), View summary(v): ").lower()

    if x == "a":
        #all variables:
        fname = input("Employee first name: ")
        lname = input("Employee last name: ")
        rnum = input("Route number: ")
        
        #open file:
        with open("Routes", "a") as t:

            #input variables into the file
            t.write(f"{fname}, {lname}, {rnum}\n")
            print("New Route Added\n")

        with open("Routes", "r") as p:
            for line in p:
                print(f"{line.strip()}")
                
        continue
            
    if x == "v":
        print("\nAll Rountes:\n")
        print("First name, Last name, Route number\n")
   
        #print all routes
        with open("Routes", "r") as p:
            for line in p:
                print(f"\n{line.strip()}")
        break

    if x == "d":     
        with open("Routes", "r") as z:

            #the list is now held in a
            a = z.readlines()

            #assigning a value to each line
            for line_number, line in enumerate(a, start=1):
                print(f"{line_number}. {line}")

            #ask which line to delete
            while True:
                delete = input("Which route would you like to delete? (Enter a number): ")
                try:
                    delete = (int(delete) -1)
                except:
                    print("Invalid Input, Try Again")
                    continue
                del a[delete]
                break
            
            #rewrite new list into the file
            with open("Routes", "w") as w:
                for line in a:
                    w.write(line)

                print("\nRoute", delete+1, "deleted\n")

        continue
    else:
        print("Invalid Input")
        continue

summary = open("Routes", 'r')
for line in summary:
    t_routes = t_routes + 1
t_cost_goods = t_routes*71000
t_payroll = t_routes*37400
other = t_routes*40000
t_expenses = t_cost_goods+t_payroll+other
t_income = t_routes*179000
net_profit = t_income - t_expenses
print()
print("Total routes: ", t_routes)
print("Cost of goods: ", t_cost_goods)
print("Total payroll: ", t_payroll)
print("Other expenses: ", other)
print("Total expenses: ", t_expenses)
print("Total income: ", t_income)
print("Net profit: ", net_profit)
input()
```
