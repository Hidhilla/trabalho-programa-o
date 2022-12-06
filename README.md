# trabalho-programa-o

import os
import json




nome_arquivo = "pacientes.json"




class bcolors:
    VERDE = '\033[92m' #GREEN
    AMARELO = '\033[93m' #YELLOW
    VERMELHO = '\033[91m' #RED
    AZUL =   '\033[94m' #AZUL
    CINZA = '\033[90m' #CINZA
    BARRAVERMELHO = '\033[101m' #BARRA VERMELHO
    BARRAVERDE = '\033[102m' #BARRA VERDE
    BARRAAMARELO = '\033[103m' #BARRA AMARELO
    BARRAAZUL = '\033[104m' #BARRA AZUL
    BARRAROSA = '\033[105m' #BARRA ROSA
    BARRAMARINHO = '\033[106m' #BARRAMARINHO
    END = '\033[0m' #END COLOR




def lerArquivo() -> list:
    arq = open(nome_arquivo, 'r', encoding='utf-8')
    pacientes = arq.read()
    return json.loads(pacientes)




def salvarArquivo(pacientes: list):
    arq = open(nome_arquivo, 'w+', encoding='utf-8')
    pacientes = json.dumps(pacientes, indent=4)
    arq.write(pacientes)
    arq.close()



def menu():
    os.system('cls')
    print(10 * '-=-')
    print(bcolors.BARRAAMARELO,'\033[93m 1 - Cadastrar Paciente:', bcolors.END)
    print(bcolors.BARRAVERDE,'\033[102m 2 - Alterar Paciente:', bcolors.END)
    print(bcolors.BARRAROSA,'\033[105m 3 - Deletar Paciente:', bcolors.END)
    print(bcolors.BARRAMARINHO,'\033[106m 4 - Selecionar Paciente por Código:', bcolors.END)
    print(bcolors.BARRAAZUL,'\033[104m 5 - Ver todos os Pacientes:', bcolors.END)

    print(10 * '-=-')
    return int(input('Escolha uma opção: '))




def cadastrarPaciente() -> dict:
    paciente = {}
    paciente['codigo'] = str(input("Código do Paciente: "))
    paciente['nome'] = str(input("Nome do Paciente: "))
    paciente['endereco'] = str(input("Endereço do Paciente:  "))
    paciente['cpf'] = str(input("CPF do Paciente: "))
    paciente['telefone'] = str(input("Telefone do Paciente: "))
    paciente['data de nascimento'] = str(input("Data de Nascimento do Paciente:  "))



    pacientes = lerArquivo()
    pacientes.append(paciente)
    salvarArquivo(pacientes)


def alterarPacientes():
    lista_json = lerArquivo()
    perdir_codigo = str(input("Código do paciente: "))
    for i in lista_json:
        if i["codigo"] == perdir_codigo:
            print(i)
            d = input("Deseja alterar o paciente ? Digite Sim para alterar e Não para sair : ")
            if d == "Sim":
                i["nome"] = input("Insira um novo nome do paciente: ")
                i["endereco"] = input("Insira um novo endereco do paciente: ")
                i["cpf"] = input("Insira um novo CPF do paciente: ")
                i["telefone"] = input("Insira um novo número de telefone do paciente: ")
                i["cpf"] = input("Insira uma nova data de nascimento do paciente: ")
    salvarArquivo(lista_json)



def deletarPacientes():
    chamar = lerArquivo()
    cod = str(input("Insira o codigo que deseja pesquisar: "))
    for i in chamar:
        if i['codigo'] == cod:
            posicao = chamar.index(i)
            chamar.pop(posicao)
    salvarArquivo(chamar)
    


def selecionarPCPacientes():
    lista_json = lerArquivo()
    pedir_codigo = str(input("Código do paciente: "))
    for i in lista_json:
        if i["codigo"] == pedir_codigo:
            print(i)
        else:
            print("Código inválido!")        
            

def mostrarPacientes():
    os.system('cls')
    print(10 * '-=-')
    arq = open(nome_arquivo, 'a+', encoding='utf-8')
    pacientes = lerArquivo()
    for paciente in pacientes:
        print(f'Código:{paciente["codigo"]}')
        print(f'Nome: {paciente["nome"]}')
        print(f'Data de nascimento: {paciente["data de nascimento"]}')
        print(f'CPF: {paciente["cpf"]}')
        print(f'Telefone: {paciente["telefone"]}')
        print(f'Endereço: {paciente["endereco"]}')

        print(10 * '-=-')


    input('Pressione ENTER para continuar...')
