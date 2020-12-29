# Clean Code
Mediante el uso de clean code y sonar qube se detectaron varios smells codes a continuacion se mencioanan algunos :

## src/main/java/pe/edu/unsa/daisi/lis/cel/config/WebSecurityConfig.java

	@Bean
	public PersistentTokenBasedRememberMeServices getPersistentTokenBasedRememberMeServices() {
		PersistentTokenBasedRememberMeServices tokenBasedservice = new PersistentTokenBasedRememberMeServices(
				"remember-me", userDetailsService, tokenRepository);

Se reemplazo por :

	@Bean
	public PersistentTokenBasedRememberMeServices getPersistentTokenBasedRememberMeServices() {
		 return new PersistentTokenBasedRememberMeServices("remember-me", userDetailsService, tokenRepository);
	}
 Debido a que la creacion de una variable temporal para devolver el objeto .
## src/main/java/pe/edu/unsa/daisi/lis/cel/config/WebSecurityConfig.java
	@Bean
	public BCryptPasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	};
La función como punto intermedio no aporta mucho ,por lo que su eliminación es plausible.

## src/main/java/pe/edu/unsa/daisi/lis/cel/config/AppJPAConfig.java
El string "hibernate.hbm2ddl.auto" se repite con cierta regularidad , esto es detectado como un smell code  que puede producir que el re-factoring mas propenso a errores y se reemplaza con una variable .

   ### private static final String ACTION_01 = "hibernate.hbm2ddl.auto";

	    props.put(SHOW_SQL, env.getRequiredProperty("hibernate.show_sql"));
	    props.put(HBM2DDL_AUTO, env.getRequiredProperty(ACTION_01));

	Properties additionalProperties() {
		Properties properties = new Properties();
		properties.setProperty(ACTION_01,env.getRequiredProperty(ACTION_01)); //create-drop
		properties.setProperty("hibernate.dialect", env.getRequiredProperty("mysql.dialect"));
		return properties;
	}
