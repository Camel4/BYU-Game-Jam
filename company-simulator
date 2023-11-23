import random

class Company:
    def __init__(self, name, stock_price, legality):
        self.name = name
        self.stock_price = stock_price
        self.legality = legality
        self.start_price = stock_price
        self.stocks = 100
        self.money = float(10000)
        self.a_owned = 0
        self.b_owned = 0
        self.c_owned = 0
        self.lives = 0
        self.crimes = 0

    def update_stock_price(self):
        # Simulate random fluctuations in stock prices
        change = random.uniform(-10, 10)
        if change == -10:
            change = -100
        elif change == 10:
            change = 100
        self.stock_price += change

    def commit_crime(self):
        # Simulate committing a crime
        if random.random() < 0.1:  # 10% chance of getting caught
            print("You got caught! Game over.")
            return True
        else:
            return False

    def price_change(self):
        percentage_change = ((self.stock_price - self.start_price) / self.start_price) * 100

        if percentage_change > 0:
            return f"+{percentage_change:.2f}%"
        elif percentage_change < 0:
            return f"{percentage_change:.2f}%"
        else:
            return f"{percentage_change:.2f}%"

    def buy_a(self, quant, price):
        self.money -= (float(quant) * price)
        self.money = round(self.money, 2)
        self.a_owned += int(quant)

    def buy_b(self, quant, price):
        self.money -= (float(quant) * price)
        self.money = round(self.money, 2)
        self.b_owned += int(quant)

    def buy_c(self, quant, price):
        self.money -= (float(quant) * price)
        self.money = round(self.money, 2)
        self.c_owned += int(quant)

    def sell_a(self, quant, price):
        self.money += (float(quant) * price)
        self.money = round(self.money, 2)
        self.a_owned -= int(quant)

    def sell_b(self, quant, price):
        self.money += (float(quant) * price)
        self.money = round(self.money, 2)
        self.b_owned -= int(quant)

    def sell_c(self, quant, price):
        self.money += (float(quant) * price)
        self.money = round(self.money, 2)
        self.c_owned -= int(quant)

def main():
    # Initialize player's company
    player_company = Company("Your Company", 100, "Legal")

    # Initialize other companies
    other_companies = [
        Company("Company A", 50, "Legal"),
        Company("Company B", 75, "Legal"),
        Company("Company C", 120, "Legal")
    ]

    while True:
        # Display game state
        player_company.update_stock_price()
        print(f"\nYour Company: {player_company.name} | Stock Price: ${player_company.stock_price:.2f} "
              f"| Change: {player_company.price_change()}")

        for other_company in other_companies:
            other_company.update_stock_price()
            print(f"{other_company.name}: ${other_company.stock_price:.2f} "
                  f"| Change: {other_company.price_change()}")

        # Player action
        print(f'You have ${player_company.money}')
        action = input("\nChoose an action (buy/sell/crime/quit/wait): ").lower()

        if action == "quit":
            break

        elif action == "wait":
            pass

        elif action == "buy":
            choice = input('Choose a Company to buy (A/B/C): ')
            for company in other_companies:
                if company.name == 'Company ' + choice:
                    quant = input(f'How many stocks of Company {choice}: ')
                    if choice == 'A':
                        player_company.buy_a(quant, company.stock_price)
                        print('\n')
                        print(f'${player_company.money} Left, Owned Stocks: {player_company.a_owned}')
                    if choice == 'B':
                        player_company.buy_b(quant, company.stock_price)
                        print('\n')
                        print(f'${player_company.money} Left, Owned Stocks: {player_company.b_owned}')
                    if choice == 'C':
                        player_company.buy_c(quant, company.stock_price)
                        print('\n')
                        print(f'${player_company.money} Left, Owned Stocks: {player_company.c_owned}')
            pass
            # Implement buying stocks logic

        elif action == "sell":
            choice = input('Choose a Company to Sell (A/B/C): ')
            choice = choice.upper()
            for company in other_companies:
                if company.name == 'Company ' + choice:
                    if choice == 'A':
                        print(f'You have {player_company.a_owned} shares of {company.name}: ')
                    if choice == 'B':
                        print(f'You have {player_company.b_owned} shares of {company.name}: ')
                    if choice == 'C':
                        print(f'You have {player_company.c_owned} shares of {company.name}: ')

                    quant = input(f'How many shares of Company {choice}: ')

                    if choice == 'A':
                        if player_company.a_owned <= int(quant) and player_company.a_owned - int(quant) > 0:
                            player_company.sell_a(quant, company.stock_price)
                            print('\n')
                            print(f'${player_company.money} Left, Owned Shares: {player_company.a_owned}')
                        else:
                            print(f'You only have {player_company.a_owned} shares of {company.name}.')

                    if choice == 'B':
                        if player_company.b_owned <= int(quant) and player_company.b_owned - int(quant) > 0:
                            player_company.sell_b(quant, company.stock_price)
                            print('\n')
                            print(f'${player_company.money} Left, Owned Shares: {player_company.b_owned}')
                        else:
                            print(f'You only have {player_company.b_owned} shares of {company.name}.')

                    if choice == 'C':
                        if player_company.c_owned <= int(quant) and player_company.c_owned - int(quant) > 0:
                            player_company.sell_c(quant, company.stock_price)
                            print('\n')
                            print(f'${player_company.money} Left, Owned Shares: {player_company.c_owned}')
                        else:
                            print(f'You only have {player_company.c_owned} shares of {company.name}.')
            pass
            # Implement selling stocks logic

        elif action == "crime":

            if player_company.legality == "Legal":
                choice = input('Do you want to commit a crime? This will remove your legal status. (y/n): ')
                if choice == 'n':
                    print("You choose to stay legal. Your stock price increases, but slowly.")
                    player_company.stock_price += random.uniform(0, 2)
                if choice == 'y':
                    print('You choose to commit a crime. This will have consequences: ')
                    player_company.legality = 'Non-Legal'
                    if player_company.commit_crime():
                        break
                    else:
                        player_company.lives += random.randint(0, 25000)
                        player_company.crimes += 1

                        player_company.stock_price += random.uniform(0, 10)
                        for company in other_companies:
                            company.stock_price -= random.uniform(0, 1)
            else:
                if player_company.commit_crime():
                    break
                else:
                    player_company.stock_price += random.uniform(0, 10)

                    player_company.lives += random.randint(0, 25000)
                    player_company.crimes += 1

                    for company in other_companies:
                        company.stock_price -= random.uniform(0, 1)


        # Check game over conditions
        if player_company.stock_price <= 0:
            print("Your company went bankrupt. Game over.")
            break
        if player_company.money <= 0:
            print('Your company ran out of money. Game over.')
            break

    # Display end game stats
    print("\nGame Over")
    print(f"Crimes Committed: {player_company.crimes}")
    print(f"Money Stolen: ${round(((float(player_company.stock_price) - float(100)) * 100), 2)}")
    print(f"Lives Ruined: {player_company.lives}")

if __name__ == "__main__":
    main()
