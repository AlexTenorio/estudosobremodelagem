# estudosobremodelagem
O estudo é meramente simples, mas com propósito de continuidade aos projetos e estudos do programa Suzano no DIO. Em breve, estarei realizando ajustes.
Criação de diagramas, script e manipulação com a ferramenta DBDesigner
# Gerar o script SQL para o modelo conceitual discutido
sql_script = """
-- Criação do Banco de Dados
CREATE DATABASE LojaRoupasMasculinas;
USE LojaRoupasMasculinas;

-- Tabela Cliente
CREATE TABLE Cliente (
    ID_Cliente INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100),
    Sobrenome VARCHAR(100),
    CPF CHAR(11),
    Telefone VARCHAR(15),
    Email VARCHAR(100),
    Endereco TEXT
);

-- Tabela Produto
CREATE TABLE Produto (
    ID_Produto INT AUTO_INCREMENT PRIMARY KEY,
    Nome_Produto VARCHAR(100),
    Categoria VARCHAR(50),
    Tamanho ENUM('P', 'M', 'G', 'GG'),
    Cor VARCHAR(50),
    Preco DECIMAL(10, 2),
    Estoque_Minimo INT
);

-- Tabela Fornecedor
CREATE TABLE Fornecedor (
    ID_Fornecedor INT AUTO_INCREMENT PRIMARY KEY,
    Nome_Fornecedor VARCHAR(100),
    Telefone VARCHAR(15),
    Email VARCHAR(100),
    CNPJ CHAR(14),
    Endereco TEXT
);

-- Tabela Estoque
CREATE TABLE Estoque (
    ID_Estoque INT AUTO_INCREMENT PRIMARY KEY,
    Quantidade INT,
    Marca VARCHAR(100),
    Data_Compra DATE,
    ID_Fornecedor INT,
    ID_Produto INT,
    Lucro DECIMAL(10, 2),
    Imposto DECIMAL(10, 2),
    FOREIGN KEY (ID_Fornecedor) REFERENCES Fornecedor(ID_Fornecedor),
    FOREIGN KEY (ID_Produto) REFERENCES Produto(ID_Produto)
);

-- Tabela Pedido
CREATE TABLE Pedido (
    ID_Pedido INT AUTO_INCREMENT PRIMARY KEY,
    Data_Pedido DATE,
    ID_Cliente INT,
    Valor_Total DECIMAL(10, 2),
    Status ENUM('Pendente', 'Pago', 'Cancelado'),
    FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID_Cliente)
);

-- Tabela Item_Pedido
CREATE TABLE Item_Pedido (
    ID_Item INT AUTO_INCREMENT PRIMARY KEY,
    ID_Pedido INT,
    ID_Produto INT,
    Quantidade INT,
    Preco_Unitario DECIMAL(10, 2),
    FOREIGN KEY (ID_Pedido) REFERENCES Pedido(ID_Pedido),
    FOREIGN KEY (ID_Produto) REFERENCES Produto(ID_Produto)
);

-- Tabela Compra_Fornecedor
CREATE TABLE Compra_Fornecedor (
    ID_Compra INT AUTO_INCREMENT PRIMARY KEY,
    Data_Compra DATE,
    ID_Fornecedor INT,
    Valor_Total DECIMAL(10, 2),
    FOREIGN KEY (ID_Fornecedor) REFERENCES Fornecedor(ID_Fornecedor)
);

-- Tabela Item_Compra
CREATE TABLE Item_Compra (
    ID_Item_Compra INT AUTO_INCREMENT PRIMARY KEY,
    ID_Compra INT,
    ID_Produto INT,
    Quantidade INT,
    Preco_Unitario DECIMAL(10, 2),
    FOREIGN KEY (ID_Compra) REFERENCES Compra_Fornecedor(ID_Compra),
    FOREIGN KEY (ID_Produto) REFERENCES Produto(ID_Produto)
);
"""

# Salvar o script SQL em um arquivo para download
file_path = "/mnt/data/LojaRoupasMasculinas.sql"
with open(file_path, "w") as file:
    file.write(sql_script)

file_path
