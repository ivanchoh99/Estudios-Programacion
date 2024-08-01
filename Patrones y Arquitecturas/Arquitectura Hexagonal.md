![[arquitectura hexagonal.png]]
La arquitectura hexagonal busca dividir nuestra aplicación por capas, donde el núcleo sea el dominio de nuestra aplicación. Buscamos que esta capa NO se acople a nada externo, mediante la inversión de dependencias nuestro dominio se acopla a contratos (interfaces o puertos) y no a implementaciones concretas.

La definición de puertos o puntos de entrada e interfaces (adaptadores) para que otros módulos puedan comunicarse sin saber el origen de los otros módulos. 

- Port (Puerto): Definición de una interfaz pública.
- Adapter (Adaptador): Especialización de un puerto para un contexto concreto.

Para ejemplificar este concepto podemos tomar esto de [Arquitectura Hexagonal con Spring Boot — Parte 2 | by Luis Antonio | Medium](https://medium.com/@oliveraluis11/arquitectura-hexagonal-con-spring-boot-parte-2-bf5371d80d20)). Nuestros puertos son:

### Ports
Aqui vemos una 

- PostCommandRepository.java
```java
public interface PostCommandRepository {  
    Optional<PostQuery> createPost(PostCommand postCommand);  
    Optional<PostQuery> updatePost(PostCommand postCommand);  
    void deletePost(int id);  
}
```

- PostQueryRepository.java
```java
public interface PostQueryRepository {  
    Optional<PostQuery> findById(int id);  
    List<PostQuery> searchBy(Map<String, String> params);  
    List<PostQuery> findAllPosts();  
}
```

### Adapters

```java 
@Repository  
@RequiredArgsConstructor  
public class PostCommandRepositoryImpl implements PostCommandRepository {  
	private final JsonPlaceholderAPIClient jsonPlaceholderAPIClient;  
	  
	@Override  
	public Optional<PostQuery> createPost(PostCommand postCommand) {  
		return Optional.ofNullable(jsonPlaceholderAPIClient.create(postCommand)); 
	}  
	  
	@Override  
	public Optional<PostQuery> updatePost(PostCommand postCommand) {  
		//Código a implementar  
		return Optional.empty();  
	}  
	  
	@Override  
	public void deletePost(int id) {  
	//Código a implementar  
	}  
}
```

```java
@Repository  
@RequiredArgsConstructor  
public class PostQueryRepositoryImpl implements PostQueryRepository {  
	private final JsonPlaceholderAPIClient jsonPlaceholderAPIClient;  
	@Override  
	public Optional<PostQuery> findById(int id) {  
		return Optional.ofNullable(jsonPlaceholderAPIClient.findPostById(id));  
	}  
	  
	@Override  
	public List<PostQuery> searchBy(Map<String, String> params) {  
		return jsonPlaceholderAPIClient.searchByParam(params);  
	}  
	  
	@Override  
	public List<PostQuery> findAllPosts() {  
		return jsonPlaceholderAPIClient.getAllPosts();  
	}  
}
```

En nuestro orden jerárquico de acceso a nuestras capas tenemos que tener en  cuenta lo siguiente:

- **Infrastructure** puede conocer a **Domain** y **Application**
- **Application** solo puede conocer a **Domain** y no a **Infrastructure**.
- **Domain** no conoce a nadie.

Teniendo esto en cuenta lo anterior tenemos nuestros adaptadores que se dividen en 2:

- Puertos de la carpeta "repository" de la capa "domain", que su implementación se encuentra en la capa "infrastructure".
- Puertos de la carpeta "service" de la capa "domain", que su implementacion se encuentra en la capa de "application"

Para acceder a los adaptadores como PostQueryRepositoryImpl, debemos emplear la inyección de dependencia y accedemos a él a través de los respectivos puertos. 
# Conceptos 
- Dominio: contexto que comprende partes fundamentales para el funcionamiento de la aplicación, como modelos, reglas, servicio y eventos.