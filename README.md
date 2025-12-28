# Pool Routes
# A Python program to manage delivery routes, allowing users to add, delete, or view routes while automatically calculating summary statistics for expenses, income, and net profit. 
t_cost_goods = 0
t_routes = 0
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
