encrypt.bat input="Niha" password=MYPAS_WORD algorithm=PBEWITHMD5ANDDES


pom.xml
		<dependency>
		    <groupId>org.jasypt</groupId>
		    <artifactId>jasypt</artifactId>
		    <version>1.9.0</version>
		</dependency>
        
   
   
   @ConfigClass
   
   import org.jasypt.encryption.StringEncryptor;
import org.jasypt.encryption.pbe.PooledPBEStringEncryptor;
import org.jasypt.encryption.pbe.config.SimpleStringPBEConfig;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

   @Bean(name = "encryptorBean")
	public StringEncryptor stringEncryptor() {
	    PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
	    SimpleStringPBEConfig config = new SimpleStringPBEConfig();
	    config.setPassword("MYPAS_WORD");
	    config.setAlgorithm("PBEWITHMD5ANDDES");
	    config.setKeyObtentionIterations("1000");
	    config.setPoolSize("1");
	    config.setProviderName("SunJCE");
	    config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator");
	    config.setStringOutputType("base64");
	    encryptor.setConfig(config);
	    return encryptor;
	}
    
    Use clsss
    
    @Autowired
	StringEncryptor encryptorBean;
    
    String decrypt1 = encryptorBean.decrypt(environment.getProperty("name"));
    
    
    ---------------------------------------------------------------------------------------------
    Get from env variables
    @Bean(name = "encryptorBean")
	public StringEncryptor stringEncryptor() {
	    PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
	    SimpleStringPBEConfig config = new SimpleStringPBEConfig();
	    System.out.println("You set :::::" + System.getenv("pass"));
	    config.setPassword(System.getenv("pass"));
	    config.setAlgorithm("PBEWITHMD5ANDDES");
	    config.setKeyObtentionIterations("1000");
	    config.setPoolSize("1");
	    config.setProviderName("SunJCE");
	    config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator");
	    config.setStringOutputType("base64");
	    encryptor.setConfig(config);
	    return encryptor;
	}
	
	
	Properties file:
	name=qQyIIgg1IUGrZrNpq/uzMg==
