import sqlite3

class Gestao:
    def __init__(self, estoque):
        self.conn = sqlite3.connect('estoque.db')
        self.criar_tabela_estoque()

    def criar_tabela_estoque(self):
        cursor = self.conn.cursor()
        cursor.execute('''
            CREATE TABLE IF NOT EXISTS estoque (
            id INTEGER PRIMARY KEY,
            produto TEXT,
            quantidade INTEGER
            )
        ''')
        self.conn.commit()

    def adicionar_produto(self, produto, quantidade):
        cursor = self.conn.cursor()
        cursor.execute(
            "INSERT INTO estoque (produto, quantidade) VALUES (?, ?)",
            (produto, quantidade))
        self.conn.commit()

    def remover_produto(self, produto, quantidade):
        cursor = self.conn.cursor()
        cursor.execute(
            "SELECT quantidade FROM estoque WHERE produto=?",
            (produto,))
        resultado = cursor.fetchone()
        if resultado:
            estoque_atual = resultado[0]
            if estoque_atual >= quantidade:
                cursor.execute("UPDATE estoque SET quantidade=? WHERE produto=?",
                               (estoque_atual - quantidade, produto))
                self.conn.commit()
            else:
                print(f"Quantidade insuficiente de {produto} em estoque")
        else:
            print(f"{produto} não encontrado em estoque")

    def consultar_estoque(self, produto):
        cursor = self.conn.cursor()
        cursor.execute(
            "SELECT quantidade FROM estoque WHERE produto=?", (produto,))
        resultado = cursor.fetchone()
        if resultado:
            return resultado[0]
        else:
            return 0

    def listar_produtos(self):
        cursor = self.conn.cursor()
        cursor.execute("SELECT produto FROM estoque")
        produtos = cursor.fetchall()
        return [produto[0] for produto in produtos]

# Exemplo de uso
sistema = Gestao("estoque.db")

sistema.adicionar_produto("Salsicha", 30)
sistema.adicionar_produto("Pão", 400)
sistema.adicionar_produto("Maionese", 10)
sistema.adicionar_produto("Milho", 5)
sistema.adicionar_produto("Ervilha", 5)
sistema.adicionar_produto("Tempero verde", 1)
sistema.adicionar_produto("Molho de tomate", 20)
sistema.adicionar_produto("Sabonete", 30)
sistema.adicionar_produto("Pasta e escova de dente", 14)
sistema.adicionar_produto("Absorvente", 22)

estoque_salsicha = sistema.consultar_estoque("Salsicha")
print(f"Quantidade de quilos de salsicha em estoque é: {estoque_salsicha}")
estoque_pao = sistema.consultar_estoque("Pão")
print(f"Quantidade de pães em estoque é: {estoque_pao}")
estoque_maionese = sistema.consultar_estoque("Maionese")
print(f"Quantidade de potes de maionese em estoque é: {estoque_maionese}")
estoque_milho = sistema.consultar_estoque("Milho")
print(f"Quantidade de potes de milho em estoque é: {estoque_milho}")
estoque_ervilha = sistema.consultar_estoque("Ervilha")
print(f"Quantidade de potes de ervilha em estoque é: {estoque_ervilha}")
estoque_tempero = sistema.consultar_estoque("Tempero verde")
print(f"Quantidade de embalagem de tempero verde em estoque é: {estoque_tempero}")
estoque_molho = sistema.consultar_estoque("Molho de tomate")
print(f"Quantidade de sache de molho em estoque é: {estoque_molho}")
estoque_sabonete = sistema.consultar_estoque("Sabonete")
print(f"Quantidade de sabonetes em estoque é: {estoque_sabonete}")
estoque_pastaeescova = sistema.consultar_estoque("Pasta e escova de dente")
print(f"Quantidade de kit pasta e escova de dente em estoque é: {estoque_pastaeescova}")
estoque_absorvente = sistema.consultar_estoque("Absorvente")
print(f"Quantidade de absorventes em estoque é: {estoque_absorvente}")

sistema.remover_produto("Absorvente", 2)

produtos_em_estoque = sistema.listar_produtos()
print("Produtos em estoque:", produtos_em_estoque)
