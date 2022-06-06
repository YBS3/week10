#Importing json
import json
#importing Pygal
import pygal
#giving file path
file_path= 'C:/Users/BhargavSai Yarlagadd/Downloads/AllStocks'
with open(file_path) as json_file:
    data_set = json.load(json_file)
    for stock in data_set:
        print(stock['symbol'], stock['date'], stock['open'], stock['high'], stock['low'], stock['close'], stock['volume'])
#creating stocks class 
class Stocks():
    def __init__(self,symbol , date, open, high, low, close, volume):
        self.symbol = symbol

        self.date = date

        self.open = open

        self.high = high

        self.low = low

        self.close = close

        self.volume = volume

# creating stocks_output sub class
    def Stocks_Output(self):
        import datetime
        today = datetime.datetime.today()
        purDate = datetime.datetime.strptime(self.purchaseDate, "%Y/%m/%d")
        NumOfDays = (today - purDate).days
        ShareGainLoss = round((self.currentPrice - self.purchasePrice), 2)
        ProfitLoss = round((ShareGainLoss * self.quantity), 2)
        YearlyProfitLoss = round((((ShareGainLoss / self.purchasePrice) / (NumOfDays / 365)) * 100), 2)
        return self.symbol + '\t' + str(self.quantity) + '\t' + str(ProfitLoss) + '\t\t' + str(YearlyProfitLoss)

# creating a new class bonds

class Bond(Stocks):
    def __init__(self, ID, symbol, quantity, purchasePrice, currentPrice, purchaseDate, Yield, coupon):
        super().__init__(ID, symbol, quantity, purchasePrice, currentPrice, purchaseDate)
        self.Yield = Yield
        self.coupon = coupon

    # defining sub class for main classs
    def Bonds_output(self):
        import datetime
        today = datetime.datetime.today()
        purDate = datetime.datetime.strptime(self.purchaseDate, "%Y/%m/%d")
        NumOfDays = (today - purDate).days
        BondGainLoss = round((self.currentPrice - self.purchasePrice), 2)
        ProfitLoss = round((BondGainLoss * self.quantity), 2)
        YearlyProfitLoss = round((((BondGainLoss / self.purchasePrice) / (NumOfDays / 365)) * 100), 2)
        return self.symbol + '\t\t' + str(self.quantity) + '\t\t\t' + str(ProfitLoss) + '\t\t\t' + str(
            YearlyProfitLoss) + '\t\t\t' + str(self.Yield) + '\t\t' + str(self.coupon)

def yearly_return_percentage(earning_loss,purchase_dt):
    
    purchase_dt=[int(value) for value in purchase_dt.split('/')]
    a=datetime.date(purchase_dt[2],purchase_dt[0],purchase_dt[1])
    now = datetime.datetime.now()
    b=datetime.date(now.year,now.month,now.day)
    return earning_loss*100.0/(b-a).days
    
def get_profit_loss(stock_data, owner):
    
    earning_loss = []
    
    for key, value in stock_data.items():
        
        difference = value[2] - value[1]
        earning_loss.append(difference * value[0])
        
    print("Stock ownership for {}".format(owner))
    print(". " * 30)
    print("STOCK \t" + "SHARE \t" + "   EARNINGS/LOSS \t" + "EARNING/LOSS")
    
    print(". " * 30)

    count = 0
    
    for key, value in stock_data.items():

        yr_per=round(yearly_return_percentage(value[2] - value[1],value[3]),2)
        print("{0:<10}{1:>4}{2:>19}{3:>15}%".format(key, value[0], '${}'.format(round(earning_loss[count], 2)),yr_per))
        count += 1
        

#improting date and time from stocks
from stock import *
import datetime

stock Dictionary = {}
for stock in data_set:
    if stock['symbol'] not in stockDictionary:
        newsymbol = symbol(stock['symbol'], stock['date'], stock['open'], stock['high'], stock['low'], stock['close'], stock['volume'])
        print ( ['symbols'] + " added")
        stockDictionary [stock ['symbol']] = newsymbol
    else:
        stockDictionary [stock ['symbol']].date = stock ['date']
        stockDictionary [stock ['symbol']].add_weight ( stock['Weight'], datetime.strptime (stock ['Date'], 'sb-sd-%Y'))
for key, stock in stockDictionary.items ():
    print (stock.symbol, stock.date, stock.open)

line_chart = pygal.Line()
line_chart.title = "Stocks Performance"
line_chart.x_labels = map(range(0, 5000, 10000, 15000, 20000, 25000) ,range(2015-7, 2015-10, 2016-1, 2016-4, 2016-7, 2016-10, 2017-4, 2017-7))
line_chart.render_to_file("simplePlot.png")

#importing uni testing

import unittest
from Week8 import Stocks

#stocks for unitesting 1
class Stocks(unittest.TestCase):
#defining test_stock_class
    def test_stock_class(self):
        inputValue = Stocks(GOOGL,25, 772.88, 941.53,'8/1/2017')
        resultValue = inputValue.profitOrLoss()
        print(resultValue)
        self.assertEqual(resultValue, 4216.25)
#defining Stocks_Purchase_date
    def Stocks_Purchase_date(self):
        inputValues = Stocks(MSFT,85, 56.60, 73.04,'8/1/2017')
        resultsValue =inputValues.yearly_return_percentage()
        print(resultsValue)
        self.assertEqual(resultsValue, 0.93%)

#defining main function
def main():
    unittest.main()


if __name__ == "__main__":
    main()
