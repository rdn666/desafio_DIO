def menu():
    menu = """
    [d] Depositar
    [s] Sacar
    [e] Extrato
    [nu] Novo Usuário
    [lu] Listar Usuários
    [nc] Nova Conta
    [lc] Lista Contas
    [q] Sair
    => """
    return(input(menu))

def saque(*,extrato, valor, numero_saques):    
    extrato += f"Saque:    R$ {valor:.2f}\n"
    numero_saques += 1
    return extrato, numero_saques

def exibir_extrato(extrato, /, *, saldo):
    print("\n================ EXTRATO ================")
    print("Não foram realizadas movimentações." if not extrato else extrato)
    print(f"\nSaldo: R$ {saldo:.2f}")
    print("==========================================")

def deposito(saldo, valor, extrato, /):
    saldo += valor
    extrato += f"Depósito: R$ {valor:.2f}\n"
    return(saldo, extrato)

def filtra_usuario(cpf, usuarios):    
    if cpf in [usuario["cpf"] for usuario in usuarios]:
        return True

def criar_usuario(usuarios):
    print('Cadastro de novo usuário')
    cpf = input('Insira o numero do CPF: ')
    if filtra_usuario(cpf, usuarios):
        print('Usuário já cadastrado')
        return
    novo_usuario = {}
    novo_usuario['cpf'] = cpf
    novo_usuario['nome'] = input('Nome: ')
    novo_usuario['data_nascimento'] = input('Data de nascimento: ')
    novo_usuario['endereco'] = input('Endereço: ')
    usuarios.append(novo_usuario)
    print('Usuario criado com sucesso')

def criar_conta(contas, usuarios, numero_agencia):
    nova_conta = {}
    numero_nova_conta = 1 if len(contas) == 0 else contas[-1]['conta'] + 1
    print(f'Cadastro de nova conta {numero_nova_conta}')
    cpf = input('Insira o numero do CPF: ')
    if filtra_usuario(cpf, usuarios):
        nova_conta['agencia'] = numero_agencia
        nova_conta['conta'] = numero_nova_conta
        nova_conta['cpf'] = cpf
        nova_conta['saldo'] = 0.0
        contas.append(nova_conta)
        print('Conta criada com sucesso')
    else:
        print('Usuário inexistente')
        return

def listar_usuarios(usuarios):
    print('\n#### Lista de Usuários ####')
    for usuario in usuarios:
        print (f'-> CPF: {usuario['cpf']}, Nome:{usuario['nome']}, Nascimento: {usuario['data_nascimento']}, Endereço: {usuario['endereco']}')

def listar_contas(contas, usuarios):
    print('\n#### Lista de Contas ####')
    cpf_para_nome = {usuario['cpf']: usuario['nome'] for usuario in usuarios}
    for conta in contas:
        print (f'-> Agencia: {conta['agencia']}, Conta: {conta['conta']}, CPF:{conta['cpf']}, Nome: {cpf_para_nome[conta['cpf']]} Saldo: {conta['saldo']:.2f}')
    

def main():
    numero_agencia = '0001'
    saldo = 0
    limite = 500
    extrato = ""
    numero_saques = 0
    LIMITE_SAQUES = 3
    usuarios = []
    contas = []
    
    while True:
    
        opcao = menu()
    
        if opcao == "d":
            valor = float(input("Informe o valor do depósito: "))
    
            if valor > 0:
                saldo, extrato = deposito(saldo, valor, extrato)
    
            else:
                print("Operação falhou! O valor informado é inválido.")
    
        elif opcao == "s":
            valor = float(input("Informe o valor do saque: "))
    
            excedeu_saldo = valor > saldo
    
            excedeu_limite = valor > limite
    
            excedeu_saques = numero_saques >= LIMITE_SAQUES
    
            if excedeu_saldo:
                print("Operação falhou! Você não tem saldo suficiente.")
    
            elif excedeu_limite:
                print("Operação falhou! O valor do saque excede o limite.")
    
            elif excedeu_saques:
                print("Operação falhou! Número máximo de saques excedido.")
    
            elif valor > 0:
                saldo -= valor
                extrato, numero_saques = saque(extrato=extrato, valor=valor, numero_saques=numero_saques)
    
            else:
                print("Operação falhou! O valor informado é inválido.")
    
        elif opcao == "e":
            exibir_extrato(extrato, saldo=saldo)

        elif opcao == 'nu':
            criar_usuario(usuarios)

        elif opcao == 'lu':
            listar_usuarios(usuarios)

        elif opcao == 'nc':
            criar_conta(contas, usuarios, numero_agencia)

        elif opcao == 'lc':
            listar_contas(contas, usuarios)
    
        elif opcao == "q":
            break
    
        else:
            print("Operação inválida, por favor selecione novamente a operação desejada.")

main()
