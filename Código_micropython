
import dht
import machine
import time
import network
import urequests

sensor = dht.DHT22(machine.Pin(15))
rale = machine.Pin(5, machine.Pin.OUT)


API_KEY = *************** ##Acesso Acadêmico.


rede = network.WLAN(network.STA_IF)
rede.active(True)
rede.connect("Wokwi-GUEST", "")

print("Conectando ao Wi-Fi...")
while not rede.isconnected():
    time.sleep(0.5)

print("Conectado! IP:", rede.ifconfig()[0])

def enviar_thingspeak(temp, umid):
    url = "http://api.thingspeak.com/update?api_key={}&field1={}&field2={}".format(API_KEY, temp, umid)
    resposta = urequests.get(url)
    print("ThingSpeak respondeu:", resposta.text)
    resposta.close()

print("Sistema iniciado")

while True:

  try:

    sensor.measure()

    temperatura = sensor.temperature()
    umidade = sensor.humidity()

    print("-----------------------")
    print("Temperatura: ", temperatura, "°C")
    print("Umidade: ", umidade, "%")

    if temperatura > 31 or umidade > 70:
      rale.value(1)
      print("Ralé: LIGADO")
    else:
      rale.value(0)
      print("Ralé: DESLIGADO")

    enviar_thingspeak(temperatura, umidade)

    time.sleep(20)

  except Exception as erro:
    print("Erro na leitura", erro)
    time.sleep(2)
