# Obligatorio2DSS

@
```
public static boolean isValidUser(String user, String password) throws SQLException {
    if (user == null || password == null || user.trim().length() == 0 || password.trim().length() == 0)
        return false;

    Connection connection = null;
    PreparedStatement preparedStatement = null;
    ResultSet resultSet = null;

    try {
        connection = getConnection();
        String query = "SELECT COUNT(*) FROM PEOPLE WHERE USER_ID = ? AND PASSWORD = ?";
        preparedStatement = connection.prepareStatement(query);
        preparedStatement.setString(1, user);
        preparedStatement.setString(2, password);

        resultSet = preparedStatement.executeQuery();

        if (resultSet.next()) {
            if (resultSet.getInt(1) > 0)
                return true;
        }
    } finally {
        // Siempre debes cerrar los recursos de la base de datos en un bloque finally
        if (resultSet != null) {
            resultSet.close();
        }
        if (preparedStatement != null) {
            preparedStatement.close();
        }
        if (connection != null) {
            connection.close();
        }
    }
    return false;
}
```
