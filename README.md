class Pessoas:
    def __init__(self,banco):
        import sqlite3
        self.conexao=sqlite3.connect('moleza.sqlite')
        self.cursor=self.conexao.cursor()

    def fechaBD(self):
        self.conexao.close()
    
    def criar_table(self):
        sql='''
            CREATE TABLE IF NOT EXISTS pessoas(
            id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
            nome TEXT NOT NULL,
            cpf INTEGER
            );
            '''
        self.cursor.execute(sql)
        print('TABELA CRIADA')

    def ler_tabela(self):
        sql='''
            SELECT * FROM pessoas;
            '''   
        resultados= self.cursor.execute(sql)
        return resultados.fetchall()
    
    def inserir_dados(self, nome,cpf):

        insercao=" INSERT INTO pessoas (nome, cpf) VALUES (?,?);"
        self.cursor.execute(insercao,[nome,cpf])
        self.conexao.commit()
        print('Dados salvos com sucesso...')

    def alterar_dados(self,nome,cpf,id):
        sql="""
            UPDATE pessoas
            SET nome= ?, cpf= ?
            WHERE ,id=?;
            """
        nome=str(input("Digite o seu nome: "))
        cpf=int(input("Digite o seu cpf: "))
        id=int(input("Digite o id: "))
        self.cursor.execute(sql,[nome,cpf,id])
        self.conexao.commit()
        print('Dados alterados...')

    def deletar_dados(self,id):
        sql="""
            DELETE FROM pessoas
            WHERE id=?;
            """
        self.cursor.execute(sql,[id])
        self.conexao.commit()
        print('Dado deletado com sucesso...')
