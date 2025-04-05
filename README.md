# Modelando o Cenário de Ordem de Serviço para Oficina Mecânica

## 📋 **Descrição do Projeto**  
Este projeto tem como objetivo modelar e implementar um sistema de controle e gerenciamento de ordens de serviço (OS) em uma oficina mecânica. A ideia é criar um banco de dados estruturado que gerencie clientes, veículos, mecânicos, serviços, peças e ordens de serviço, garantindo o acompanhamento detalhado do processo desde a criação da OS até a sua conclusão.

---

## 📐 **Estrutura Conceitual**  
A modelagem segue os seguintes conceitos principais:

- **Cliente:** Representa os clientes que levam seus veículos para a oficina.  
- **Veículo:** Os automóveis trazidos pelos clientes para manutenção ou revisão.  
- **Ordem de Serviço (OS):** Gerencia os serviços realizados em cada veículo, incluindo peças utilizadas e valores.  
- **Serviço:** Tipos de tarefas realizadas pelos mecânicos, como troca de óleo ou revisão de freios.  
- **Peça:** Itens usados para reparos ou manutenção dos veículos.  
- **Mecânico:** Equipe responsável por avaliar e executar os serviços relacionados às ordens de serviço.  

---

## 🛠️ **Entidades e Relacionamentos**  

### **Entidades**
1. **Cliente:**  
   Contém informações como nome, CPF, telefone e endereço.  

2. **Veículo:**  
   Inclui atributos como placa, modelo, marca, ano e vínculo com o cliente.  

3. **Ordem de Serviço (OS):**  
   Registra os serviços realizados, peças utilizadas, data de emissão, status e valor total.  

4. **Serviço:**  
   Contém os tipos de atividades realizadas, como troca de óleo e manutenção periódica.  

5. **Peça:**  
   Registra os itens utilizados na OS, como filtros de óleo ou pastilhas de freio.  

6. **Mecânico:**  
   Contém informações como nome, endereço e especialidade.  

7. **OS_Servico:** *(Entidade Associativa)*  
   Relaciona uma OS aos serviços realizados.  

8. **OS_Peca:** *(Entidade Associativa)*  
   Relaciona uma OS às peças utilizadas.  

9. **Equipe_Mecanico:** *(Entidade Associativa)*  
   Vincula mecânicos a ordens de serviço específicas.  

---

### **Relacionamentos**
- **Cliente possui Veículo (1:N)**  
- **Veículo tem Ordem de Serviço (1:N)**  
- **Ordem de Serviço inclui Serviço (N:M)** *(via OS_Servico)*  
- **Ordem de Serviço utiliza Peça (N:M)** *(via OS_Peca)*  
- **Ordem de Serviço é executada por Mecânico (N:M)** *(via Equipe_Mecanico)*  

---

## 📦 **Tecnologias Utilizadas**  
- **MySQL:** Banco de dados relacional para criar e gerenciar tabelas e relacionamentos.  
- **Workbench:** Ferramenta gráfica para modelagem e execução de comandos SQL.  

---

## 💡 **Arquitetura do Banco de Dados**  
As tabelas possuem características como:  
- **Chaves primárias auto incrementadas:** Para identificar entidades de forma única.  
- **Chaves estrangeiras:** Garantem integridade referencial entre as tabelas.  
- **Tipos de dados otimizados:** Uso de VARCHAR, DECIMAL, DATETIME, etc.  
- **Estrutura escalável:** Suporte para futuras expansões e ajustes.

---

## 📄 **Comandos Importantes**

### Exemplo: Criação de tabelas com chaves primárias e estrangeiras
```sql
CREATE TABLE Veiculo (
    ID_Veiculo INT NOT NULL AUTO_INCREMENT,
    Placa VARCHAR(7) NOT NULL,
    Modelo VARCHAR(100),
    Marca VARCHAR(50),
    Ano YEAR NOT NULL,
    ID_Cliente INT NOT NULL,
    PRIMARY KEY (ID_Veiculo),
    FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID_Cliente)
);

CREATE TABLE Ordem_Servico (
    ID_OS INT NOT NULL AUTO_INCREMENT,
    Data_Emissao DATETIME DEFAULT CURRENT_TIMESTAMP,
    Valor_Total DECIMAL(10,2) NOT NULL,
    Status ENUM('Aberta', 'Em andamento', 'Concluída') NOT NULL,
    Data_Conclusao DATETIME,
    ID_Veiculo INT NOT NULL,
    PRIMARY KEY (ID_OS),
    FOREIGN KEY (ID_Veiculo) REFERENCES Veiculo(ID_Veiculo)
);
```
Exemplo: Relacionamento N:M entre Ordem de Serviço e Serviço
```sql
CREATE TABLE OS_Servico (
    ID_OSServico INT AUTO_INCREMENT PRIMARY KEY,
    ID_OS INT NOT NULL,
    ID_Servico INT NOT NULL,
    FOREIGN KEY (ID_OS) REFERENCES Ordem_Servico(ID_OS),
    FOREIGN KEY (ID_Servico) REFERENCES Servico(ID_Servico)
);
```
## **🌟 Contribuições:**
Sinta-se à vontade para sugerir melhorias ou compartilhar suas ideias!

  <p align="center">
  Copyright © 2024. Desenvolvido com 🧡 por <a  href="https://lirazootech.vercel.app/">Thays Lira</a>.
  </p>

