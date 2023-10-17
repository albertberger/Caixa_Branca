# Documentação

## Código documentado

package login;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

/**
 * Classe que representa um usuário e sua conexão com o banco de dados.
 */
public class User {

    /**
     * Estabelece uma conexão com o banco de dados.
     *
     * @return A conexão com o banco de dados.
     */
    public Connection conectarBD() {
        Connection conn = null; // Inicializa a conexão como nula
        try {
            Class.forName("com.mysql.Driver.Manager").newInstance(); // Carrega o driver do MySQL
            String url = "jdbc:mysql://127.0.0.1/test?user=lopes&password=123"; // Caminho para o banco de dados
            conn = DriverManager.getConnection(url); // Estabelece a conexão com o banco de dados
        } catch (Exception e) {
            // Tratamento de exceção caso ocorra um erro na conexão com o banco de dados
        }
        return conn; // Retorna a conexão com o banco de dados
    }

    public String nome = ""; // Nome de usuário

    public boolean result = false; // Indica se a busca de usuário retornou um resultado

    /**
     * Verifica se um usuário está registrado no banco de dados.
     *
     * @param login O login do usuário.
     * @param senha A senha do usuário.
     * @return true se o usuário está registrado, false caso contrário.
     */
    public boolean verificarUsuario(String login, String senha) {
        String sql = ""; // Inicializa a variável SQL como uma string vazia

        Connection conn = conectarBD(); // Conecta-se ao banco de dados

        // Monta a consulta SQL para buscar o usuário
        sql += "select nome from usuarios";
        sql += " where login = '" + login + "'";
        sql += " and senha = '" + senha + "';";

        try {
            // Executa a consulta SQL
            Statement st = conn.createStatement();
            ResultSet rs = st.executeQuery(sql);

            // Se o usuário for encontrado, atualiza os resultados
            if (rs.next()) {
                result = true;
                nome = rs.getString("nome");
            }
        } catch (Exception e) {
            // Tratamento de exceção em caso de erro na busca do usuário no banco de dados
        }

        return result; // Retorna o resultado da busca do usuário
    }
} 
