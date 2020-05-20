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




<svg width="508" height="130" xmlns="http://www.w3.org/2000/svg">
 <!-- Created with Method Draw - http://github.com/duopixel/Method-Draw/ -->
 <g>
  <title>background</title>
  <rect fill="none" id="canvas_background" height="132" width="510" y="-1" x="-1"/>
  <g display="none" overflow="visible" y="0" x="0" height="100%" width="100%" id="canvasGrid">
   <rect fill="url(#gridpattern)" stroke-width="0" y="0" x="0" height="100%" width="100%"/>
  </g>
 </g>
 <g>
  <title>Layer 1</title>
  <path stroke="#00ffff" id="svg_1" d="m4.017512,3.475756l143.249931,0l47.75006,61.499866l-47.75006,61.500138l-143.249931,0l47.750047,-61.500138l-47.750047,-61.499866z" stroke-width="3.5" fill="none"/>
  <path stroke="#00ffff" id="svg_2" d="m159.01751,3.47576l143.24993,0l47.75006,61.49986l-47.75006,61.50014l-143.24993,0l47.75005,-61.50014l-47.75005,-61.49986z" stroke-width="3.5" fill="none"/>
  <path stroke="#00ffff" id="svg_3" d="m313.01751,3.47576l143.24993,0l47.75006,61.49986l-47.75006,61.50014l-143.24993,0l47.75005,-61.50014l-47.75005,-61.49986z" stroke-width="3.5" fill="none"/>
  <text font-weight="normal" xml:space="preserve" text-anchor="start" font-family="Arvo, sans-serif" font-size="21" id="svg_4" y="72.85" x="93.5" stroke-width="0" stroke="#00ffff" fill="#00ffff">New</text>
  <text font-weight="normal" xml:space="preserve" text-anchor="start" font-family="Arvo, sans-serif" font-size="21" id="svg_5" y="72.85" x="217.5" stroke-width="0" stroke="#00ffff" fill="#00ffff">In Progress</text>
  <text style="cursor: move;" font-weight="normal" xml:space="preserve" text-anchor="start" font-family="Arvo, sans-serif" font-size="21" id="svg_6" y="72.85" x="397.5" stroke-width="0" stroke="#00ffff" fill="#00ffff">Close</text>
 </g>
</svg>
