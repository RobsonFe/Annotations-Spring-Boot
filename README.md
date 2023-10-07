# Annotations-Spring-Boot
Essa documentação tem a finalidade de exemplificar e trazer informações sobre as annotations mais usadas no Spring Boot.

Abaixo, você encontrará as explicações das 21 annotations do Spring Boot, juntamente com exemplos de código para cada uma delas:

### 1. `@Component`:

- **Explicação**: A annotation `@Component` é usada para indicar que uma classe é um componente gerenciado pelo Spring. Isso significa que o Spring irá detectar automaticamente essa classe e registrá-la como um bean no contexto da aplicação.

```java
@Component
public class MyComponent {
    // Código da classe
}
```

### 2. `@Service`, `@Repository`, `@Controller`, `@RestController`:

- **Explicação**: Essas annotations são especializações de `@Component`. Elas são usadas para definir tipos específicos de beans gerenciados pelo Spring. Por exemplo, `@Service` é usado para marcar serviços, `@Repository` para repositórios de dados, `@Controller` para controladores da web e `@RestController` combina `@Controller` com `@ResponseBody`.

```java
@Service
public class MyService {
    // Código do serviço
}
```

### 3. `@Autowired`:

- **Explicação**: A annotation `@Autowired` é usada para injetar dependências automaticamente em um bean. O Spring resolverá automaticamente as dependências e as injetará quando o bean for criado.

```java
@Service
public class MyService {
    private final MyRepository repository;

    @Autowired
    public MyService(MyRepository repository) {
        this.repository = repository;
    }
}
```

### 4. `@Qualifier`:

- **Explicação**: A annotation `@Qualifier` é usada junto com `@Autowired` para especificar qual bean exato deve ser injetado quando existem várias implementações possíveis.

```java
@Service
public class MyService {
    private final MyRepository repository;

    @Autowired
    public MyService(@Qualifier("myRepositoryImpl") MyRepository repository) {
        this.repository = repository;
    }
}
```

### 5. `@Value`:

- **Explicação**: A annotation `@Value` é usada para injetar valores de propriedade diretamente em um bean, em vez de depender de um arquivo de propriedades externo.

```java
@Component
public class MyComponent {
    @Value("${my.property}")
    private String myProperty;
}
```

### 6. `@Configuration`:

- **Explicação**: A annotation `@Configuration` é usada para indicar que uma classe é uma classe de configuração do Spring. Ela geralmente contém definições de beans e configurações específicas da aplicação.

```java
@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

### 7. `@ComponentScan`:

- **Explicação**: A annotation `@ComponentScan` é usada para especificar os pacotes que o Spring deve escanear em busca de componentes gerenciados.

```java
@Configuration
@ComponentScan("com.example")
public class MyConfiguration {
    // Configuração personalizada
}
```

### 8. `@Bean`:

- **Explicação**: A annotation `@Bean` é usada em métodos dentro de classes anotadas com `@Configuration`. Ela indica que o método produz um bean que será gerenciado pelo Spring.

```java
@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

### 9. `@Lazy`:

- **Explicação**: A annotation `@Lazy` é usada para indicar que um bean deve ser inicializado de forma preguiçosa, ou seja, somente quando for necessário.

```java
@Component
@Lazy
public class MyLazyComponent {
    // Código do componente
}
```

### 10. `@Primary`:

- **Explicação**: A annotation `@Primary` é usada quando há várias implementações possíveis de um bean. Ela indica que uma implementação específica deve ser considerada como a principal quando houver conflitos de resolução de dependência.

```java
@Service
@Primary
public class MyPrimaryService implements MyService {
    // Código do serviço principal
}
```

### 11. `@Scope`:

- **Explicação**: A annotation `@Scope` é usada para definir o escopo de um bean, ou seja, quando e como o bean deve ser criado e destruído.

```java
@Component
@Scope("prototype")
public class MyPrototypeComponent {
    // Código do componente de escopo de protótipo
}
```

### 12. `@PropertySource` e `@PropertySources`:

- **Explicação**: `@PropertySource` é usada para especificar um arquivo de propriedades externo que deve ser carregado como fonte de propriedades. `@PropertySources` permite a configuração de várias fontes de propriedades

.

```java
@Configuration
@PropertySource("classpath:my-config.properties")
public class MyConfiguration {
    // Configuração personalizada
}
```

### 13. `@Profile`:

- **Explicação**: A annotation `@Profile` é usada para ativar ou desativar componentes específicos com base em perfis de aplicação ativos.

```java
@Component
@Profile("dev")
public class MyDevComponent {
    // Código do componente para o perfil "dev"
}
```

### 14. `@SpringBootApplication`:

- **Explicação**: `@SpringBootApplication` é uma annotation composta que combina várias outras annotations, incluindo `@Configuration`, `@ComponentScan`, e `@EnableAutoConfiguration`. Ela é usada para marcar a classe principal da aplicação Spring Boot.

```java
@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

### 15. `@EnableAutoConfiguration`:

- **Explicação**: A annotation `@EnableAutoConfiguration` é usada para permitir que o Spring Boot configure automaticamente componentes e dependências com base nas bibliotecas e no ambiente de execução detectados.

```java
@SpringBootApplication
public class MySpringBootApplication {
    // Configuração personalizada
}
```

### 16. `@ConfigurationProperties`:

- **Explicação**: A annotation `@ConfigurationProperties` é usada para vincular propriedades de configuração a um bean personalizado. Ela permite que você injete configurações diretamente em classes Java.

```java
@Configuration
@ConfigurationProperties(prefix = "my")
public class MyConfigProperties {
    private String property1;
    private int property2;
    // Getters e setters
}
```

### 17. `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@DeleteMapping`, `@PutMapping`:

- **Explicação**: Essas annotations são usadas para mapear métodos de controladores da web para URLs específicas, definindo os métodos HTTP correspondentes.

```java
@RestController
@RequestMapping("/api")
public class MyRestController {
    @GetMapping("/resource")
    public ResponseEntity<String> getResource() {
        // Lógica do controlador
    }
}
```

### 18. `@RequestBody`:

- **Explicação**: A annotation `@RequestBody` é usada para indicar que um parâmetro de método deve ser vinculado ao corpo da solicitação HTTP em um controlador da web.

```java
@RestController
@RequestMapping("/api")
public class MyRestController {
    @PostMapping("/create")
    public ResponseEntity<String> createResource(@RequestBody Resource resource) {
        // Lógica do controlador para criar um recurso com base no corpo da solicitação
    }
}
```

### 19. `@PathVariable`:

- **Explicação**: A annotation `@PathVariable` é usada para vincular variáveis de caminho (por exemplo, `/{id}`) a parâmetros de método em controladores da web.

```java
@RestController
@RequestMapping("/api")
public class MyRestController {
    @GetMapping("/resource/{id}")
    public ResponseEntity<String> getResourceById(@PathVariable Long id) {
        // Lógica do controlador para buscar um recurso com base no ID no caminho
    }
}
```

### 20. `@RequestParam`:

- **Explicação**: A annotation `@RequestParam` é usada para vincular parâmetros de consulta (por exemplo, `?name=John`) a parâmetros de método em controladores da web.

```java
@RestController
@RequestMapping("/api")
public class MyRestController {
    @GetMapping("/search")
    public ResponseEntity<String> searchResource(@RequestParam String keyword) {
        // Lógica do controlador para buscar recursos com base no parâmetro de consulta
    }
}
```

### 21. `@CrossOrigin`:

- **Explicação**: A annotation `@CrossOrigin` é usada para permitir solicitações de origens diferentes (CORS) em um controlador da web.

```java
@RestController
@RequestMapping("/api")
@CrossOrigin(origins = "http://localhost:8080")
public class MyRestController {
    // Lógica do controlador
}
```

Esses exemplos de código devem ajudar a ilustrar o uso de cada annotation do Spring Boot em situações práticas.
