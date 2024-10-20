# sistema-bancario_modificado
class ContaBancaria:
    def __init__(self, titular, saldo=0):
        self.titular = titular
        self.saldo = saldo

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            print(f"Depósito de R${valor:.2f} realizado com sucesso!")
        else:
            print("Valor inválido para depósito.")

    def sacar(self, valor):
        if 0 < valor <= self.saldo:
            self.saldo -= valor
            print(f"Saque de R${valor:.2f} realizado com sucesso!")
        else:
            print("Saldo insuficiente ou valor inválido para saque.")

    def verificar_saldo(self):
        print(f"Saldo atual de {self.titular}: R${self.saldo:.2f}")

    def transferir(self, valor, conta_destino):
        if 0 < valor <= self.saldo:
            self.saldo -= valor
            conta_destino.saldo += valor
            print(f"Transferência de R${valor:.2f} para {conta_destino.titular} realizada com sucesso!")
        else:
            print("Saldo insuficiente ou valor inválido para transferência.")


def exibir_menu():
    print("\n=== Sistema Bancário ===")
    print("1. Criar Conta")
    print("2. Depositar")
    print("3. Sacar")
    print("4. Verificar Saldo")
    print("5. Transferir")
    print("6. Sair")


def encontrar_conta(titular, contas):
    return next((c for c in contas if c.titular == titular), None)


def main():
    contas = []

    while True:
        exibir_menu()
        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            nome = input("Nome do titular: ")
            conta = ContaBancaria(nome)
            contas.append(conta)
            print(f"Conta criada com sucesso para {nome}!")

        elif opcao in ('2', '3', '4', '5'):
            nome = input("Nome do titular: ")
            conta = encontrar_conta(nome, contas)
            if conta:
                if opcao == '2':
                    valor = float(input("Valor a depositar: "))
                    conta.depositar(valor)
                elif opcao == '3':
                    valor = float(input("Valor a sacar: "))
                    conta.sacar(valor)
                elif opcao == '4':
                    conta.verificar_saldo()
                elif opcao == '5':
                    nome_destino = input("Nome do titular (Conta de destino): ")
                    conta_destino = encontrar_conta(nome_destino, contas)
                    if conta_destino:
                        valor = float(input("Valor a transferir: "))
                        conta.transferir(valor, conta_destino)
                    else:
                        print("Conta de destino não encontrada.")
            else:
                print("Conta não encontrada.")

        elif opcao == '6':
            print("Saindo do sistema bancário. Até logo!")
            break

        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    main()
