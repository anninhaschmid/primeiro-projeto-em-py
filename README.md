# primeiro-projeto-em-py
sistema de notas 
# Dicionário para armazenar as informações dos alunos
estudantes = {}

# Função para cadastrar um estudante
def cadastrar_estudante():
    matricula = input("Digite a matrícula do estudante: ")
    nome = input("Digite o nome do estudante: ")
    estudantes[matricula] = {'nome': nome, 'notas': []}
    print(f"Estudante {nome} cadastrado com sucesso!\n")

# Função para adicionar notas de um estudante
def adicionar_notas():
    matricula = input("Digite a matrícula do estudante: ")
    
    if matricula not in estudantes:
        print("Estudante não encontrado!\n")
        return
    
    notas = []
    for i in range(3):  # Limite de 3 notas
        while True:
            try:
                nota = float(input(f"Digite a nota {i+1} do estudante: "))
                if 0 <= nota <= 10:
                    notas.append(nota)
                    break
                else:
                    print("Nota inválida! Deve ser entre 0 e 10.")
            except ValueError:
                print("Por favor, insira um número válido para a nota.")
    
    estudantes[matricula]['notas'] = notas
    print(f"Notas do estudante {estudantes[matricula]['nome']} atualizadas com sucesso!\n")

# Função para calcular a média e verificar a aprovação
def calcular_media():
    matricula = input("Digite a matrícula do estudante: ")
    
    if matricula not in estudantes:
        print("Estudante não encontrado!\n")
        return
    
    notas = estudantes[matricula]['notas']
    
    if len(notas) == 0:
        print(f"O estudante {estudantes[matricula]['nome']} não tem notas registradas.\n")
        return
    
    media = sum(notas) / len(notas)
    status = "Aprovado" if media >= 6 else "Reprovado"
    print(f"Média do estudante {estudantes[matricula]['nome']}: {media:.2f} ({status})\n")

# Função para listar todos os estudantes
def listar_estudantes():
    if not estudantes:
        print("Nenhum estudante cadastrado.\n")
        return
    
    print("Lista de Estudantes:")
    for matricula, info in estudantes.items():
        nome = info['nome']
        notas = info['notas']
        if notas:
            media = sum(notas) / len(notas)
            status = "Aprovado" if media >= 6 else "Reprovado"
            print(f"{nome} - Matrícula: {matricula} - Média: {media:.2f} ({status})")
        else:
            print(f"{nome} - Matrícula: {matricula} - Sem notas cadastradas.")

# Função principal que vai exibir o menu
def menu():
    while True:
        print("1. Cadastrar Estudante")
        print("2. Adicionar Notas")
        print("3. Calcular Média")
        print("4. Listar Estudantes")
        print("5. Sair")
        
        opcao = input("Escolha uma opção: ")
        
        if opcao == '1':
            cadastrar_estudante()
        elif opcao == '2':
            adicionar_notas()
        elif opcao == '3':
            calcular_media()
        elif opcao == '4':
            listar_estudantes()
        elif opcao == '5':
            print("Saindo do sistema...")
            break
        else:
            print("Opção inválida! Tente novamente.\n")

# Iniciar o sistema
menu()
