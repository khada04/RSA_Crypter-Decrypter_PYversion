# RSA_Crypter-Decrypter_PYversion
RSA.py es una version pensada para windows, con pocas modificaciones deberia funcionar bien en linux.
El codigo esta documentado, sientete libre de usarlo/modificarlo :')


from Crypto.Util.number import *
from Crypto import Random
import Crypto
import sys
import os
############################ Generando llaves ############################
print("############################# Programa de encriptacion y desencritacion RSA #############################\n")
print("                   Seleccione: 1(Encriptacion)  2(Desencriptacion) 3(Cerrar el programa)")

INICIO=int(input("Que desea hacer?: "))
while(INICIO<1 or INICIO>3):
    os.system("cls")
    print("se ha introducido un valor invalido, por favor seleccione una de las funciones dadas anteriormente")
    print("                   Seleccione: 1(Encriptacion)  2(Desencriptacion) 3(Cerrar el programa)")
    INICIO=int(input("Que desea hacer?: "))

##Cifrando el mensaje 
if(INICIO==1):
    BITS=int(input("RSA key and can be configured from 360 bits to 4,096 bits: "))
    MSG_LL=input("Mensaje que quiere cifrar: ")
    PP = Crypto.Util.number.getPrime(BITS, randfunc=Crypto.Random.get_random_bytes)
    SP = Crypto.Util.number.getPrime(BITS, randfunc=Crypto.Random.get_random_bytes)
    N = PP*SP  #Se usara como modulo tanto para la llave publica como para la privada 
    PHI=(PP-1)*(SP-1) # función φ de Euler 
    E=65537 #Exponente de llave privada 
    MSG_NUM= bytes_to_long(MSG_LL.encode('utf-8'))### SE LLEVA EL MENSAJE LLANO A FORMA NUMERICA ###
    MSG_C=pow(MSG_NUM,E, N)
    D=inverse(E,PHI) #Exponente llave privada
    print("Su mensaje en forma numerica es: ",MSG_NUM)
    print("")
    print("La forma numerica CIFRADA de su mensaje es: ", MSG_C)
    print("")
    print("El exponenete de su llave privada es: ", D ,"Recuerde mantener esta informacion en secreto.")
    print("")
    print("El Modulo de las llaves privada y publica es: ", N, "Recuerde mantener esta informacion en secreto")
    fin=input("Fin del programa")

if(INICIO==2):
    print("Eligio la opcion de desencriptar un mensaje ya encriptado anteriormente, por favor suministre los datos siguientes: ")
    MSG_C1=input("Mensaje cifrado: ")
    MSG_C2=int(MSG_C1)
    print("")
    D1=input("Exponente de la llave privada: ")
    D2=int(D1)
    print("")
    N1=input("Modulo de las llaves publica y privada: ")
    N2=int(N1)    
    MSG_D=pow(MSG_C2,D2, N2)
    print("")
    print("La forma numerica de su mensaje es: ", MSG_D)
    MSG_LLD=long_to_bytes(MSG_D)
    print("Su mensaje descifrado es: ", MSG_LLD)
    fin=input("Fin del programa")

if(INICIO==3):
    fin=input("Fin del programa")
