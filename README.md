# Caixa_Branca

#Código

1.package login; 

1.import java.sql.Connection;
1.import java.sql.DriverManager;
1.import java.sql.ResultSet;
1.import java.sql.Statment;

2.public class User{
    3.public Connection conectarBD(){
        4.	Connection conn = null;
        5.try{
           6. Class.forName("com.mysql.Driver.Manager").newInstance();
            6.String url = "jdbc:mysql://127.0.0.1/test?user=lopes&password=123";
            6. conn = DriverManager.getConnection(url);
        7.}  8. catch 9. (Exception e) { } 
       10. return conn; 
11.}
12.public String nome= "";
12.public boolean result = false;
13. public boolean verificarUsuario (String login, String senha){
    14. String sql = "";
    14.Connection conn = conectarBD();

    14. sql += "select nome from usuarios";
    14. sql += "where login = " + "'" + login + "'";
    14. sql += "and senha = " + "'" + senha + "';";
    15 .try{		
        16. Statment st = conn.createStatement();
        16. ResultSet rs = st.executeQuery(sql);
        17. if (rs.next()){
            18.result = true;
            18. nome = rs.getString("nome");
19.}
    20.} 21.catch  22.(Exception e) { }
    23. return result;}
24.
