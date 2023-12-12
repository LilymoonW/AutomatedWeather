import requests
from requests_html import HTMLSession
import datetime
import schedule
import time

location = 'Wellesley'
def sendMessege():
    resp = requests.post('https://textbelt.com/text', {
        'phone': '4255889086',
        'message': constructMessage() ,
        'key': 'textbelt',
    })
    print(resp.json())
def constructMessage():
    now = str(datetime.date.today())
    body = "Good Morning! Today is " + now + "\n"
    weather = getWeather()
    temp = getTemp()
    body += weather + '\n'
    if 'rain' in weather:
        body += 'Don\'t forget to bring an umbrella!\n'
    if int(temp) <= 32:
        body += 'BRrrrr it\'s FREEZING! Don\'t forget to dress warm!\n'
    if 'sunny' in weather and int(temp) >= 70:
        body += 'It\'s going to be HOT!!! Make sure you apply sunscreen!\n'
    if 'Snow' in weather:
        body += 'It\'s SNOWING!!! Make sure you dress warm and BUILD a Snowman!\n'
    return body
def getWeather():
    s = HTMLSession()
    urlWeather = f'https://www.google.com/search?q=weather+{location}'
    r = s.get(urlWeather, headers={'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, '
                                                 'like Gecko) Chrome/119.0.0.0 Safari/537.36'})
     temp = r.html.find('span#wob_tm', first=True).text
    unitOfMeasurement = r.html.find('div.vk_bk.wob-unit span.wob_t', first=True).text
    conditions = r.html.find('span#wob_dc', first=True).text
    return location + ' ' + temp + ' ' + unitOfMeasurement + ' ' + conditions
def getTemp():
    body = getWeather().split()
    for i in body:
        if i.isdigit():
            return i

print(constructMessage())

schedule.every().monday.at('08:15').do(sendMessege())
schedule.every().tuesday.at('10:30').do(sendMessege())
schedule.every().wednesday.at('08:15').do(sendMessege())
schedule.every().thursday.at('08:15').do(sendMessege())
schedule.every().friday.at('10:30').do(sendMessege())
while True:
    schedule.run_pending()
    time.sleep(1)

