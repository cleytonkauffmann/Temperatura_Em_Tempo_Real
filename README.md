Temperatura_Em_Tempo_Real
Consulte a temperatura de sua cidade

import requests from bs4 import BeautifulSoup

def obter_temperatura_google(cidade): url = f"https://www.google.com/search?q=temperatura+{cidade}" headers = { "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"} response = requests.get(url, headers=headers) if response.status_code == 200: soup = BeautifulSoup(response.text, 'html.parser') temperatura_fahrenheit = soup.find("div", class_="BNeawe iBp4i AP7Wnd").get_text() temperatura_celsius = converter_para_celsius(temperatura_fahrenheit) return temperatura_celsius else: return None

def converter_para_celsius(temperatura_fahrenheit): temperatura_fahrenheit = temperatura_fahrenheit.replace("°F", "") # Remover o símbolo de Fahrenheit temperatura_celsius = (float(temperatura_fahrenheit) - 32) * 5/9 # Converter Fahrenheit para Celsius return round(temperatura_celsius, 2)

Exemplo de uso:
cidade = input("Digite o nome da cidade: ")

temperatura = obter_temperatura_google(cidade) if temperatura: print(f"A temperatura em {cidade} é {temperatura}°C") else: print("Não foi possível obter a temperatura. Verifique se o nome da cidade está correto.")
