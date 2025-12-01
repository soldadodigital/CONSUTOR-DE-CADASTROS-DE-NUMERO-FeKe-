import random
import time
import re  
import sys  

def validar_numero_telefone(numero):
    """Valida se o número tem DDD ou código do país (+55)."""
    
    numero_limpo = re.sub(r'[^\d+]', '', numero.strip())

    if numero_limpo.startswith('+55'):
        
        if len(numero_limpo) >= 13:
            return True
    elif len(numero_limpo) >= 10:  
        return True
    return False

def gerar_resposta():
    """Gera e retorna um CPF, CNPJ e endereço aleatórios (como strings simples)."""
   
    cpf = ''.join(str(random.randint(0, 9)) for _ in range(11))
    cpf_formatado = f"{cpf[:3]}.{cpf[3:6]}.{cpf[6:9]}-{cpf[9:]}"

    cnpj = ''.join(str(random.randint(0, 9)) for _ in range(14))
    cnpj_formatado = f"{cnpj[:2]}.{cnpj[2:5]}.{cnpj[5:8]}/{cnpj[8:12]}-{cnpj[12:]}"

    endereco = ''.join(str(random.randint(0, 9)) for _ in range(8))
    endereco_formatado = f"{endereco[:5]}-{endereco[5:]}"

    return {
        "CPF": cpf_formatado,
        "CNPJ": cnpj_formatado,
        "Endereço (CEP)": endereco_formatado
    }

def animacao_carregamento(duracao_segundos=8, mensagem="Consultando dados..."):
    """Exibe uma animação de spinner durante o tempo de espera."""
    spinner = ['|', '/', '-', '\\']
    for i in range(duracao_segundos * 2):  
        
        sys.stdout.write(f"\r{mensagem} {spinner[i % 4]}")
        sys.stdout.flush()
        time.sleep(0.5) 
    sys.stdout.write("\r" + " " * (len(mensagem) + 2) + "\r")  


print("="  * 50 ) 
print("         ⛾ 𝓢ᴅɴ𝓒 ⛾")
print("=" * 50)
print("𝐁𝐄𝐌-𝐕𝐈𝐍𝐃𝐎 ao 𝐒𝐈𝐒𝐓𝐄𝐌𝐀 𝐃𝐄 𝐂𝐎𝐍𝐒𝐔𝐓𝐀♘♘♘!")
print("- CPF (Cadastro de Pessoa Física)")
print("- CNPJ (Cadastro Nacional da Pessoa Jurídica)")
print("- Endereço (CEP simples)")
print("Digite um número para começar. Exemplo: 11987654321 ou +5511987654321")
print("=" * 50)

while True:
    
    numero_digitado = input("Digite um número: ")
    print(f"Você digitou: {numero_digitado}")

 
    if not validar_numero_telefone(numero_digitado):
        print("O número não é verdadeiro (não possui DDD ou código do país válido).")
    else:
       
        animacao_carregamento(8, "Aguarde um momento...")

        resultados = gerar_resposta()
        print("\nResultados gerados:")
        for chave, valor in resultados.items():
            print(f"{chave}: {valor}")

    while True:
        opcao = input("\nDeseja consultar outro número? (s/n): ").strip().lower()
        if opcao in ['s', 'sim']:
            print("\n" + "=" * 50)  
            break  
        elif opcao in ['n', 'não', 'nao']:
            print("Obrigado por usar o sistema! Até logo.")
            exit()  
        else:
            print("Opção inválida. Digite 's' para sim ou 'n' para não.")
