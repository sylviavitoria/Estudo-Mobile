# Estudo-Mobile


# 📱 CONCEITO GERAL SOBRE DESENVOLVIMENTO MOBILE

O desenvolvimento mobile é a criação de aplicativos que rodam em dispositivos móveis, como smartphones e tablets. Existem dois principais sistemas operacionais:

- **Android (Google)**
- **iOS (Apple)**

---

## 🎯 Tipos de desenvolvimento

| Tipo            | Descrição                                                                 |
|------------------|--------------------------------------------------------------------------|
| **Nativo**       | Código específico para cada sistema. Melhor desempenho e acesso total aos recursos do dispositivo. |
| **Multiplataforma** | Código único que gera app para Android e iOS. Menor custo, mas pode ter limitações de desempenho ou acesso a recursos nativos. |

---

## 💬 COMPARATIVO ENTRE TECNOLOGIAS

| Tecnologia     | Linguagem             | Plataforma     | Tipo             | IDE / Ferramenta         |
|----------------|------------------------|----------------|------------------|---------------------------|
| Kotlin         | Kotlin                | Android        | Nativo           | Android Studio            |
| Swift          | Swift                 | iOS            | Nativo           | Xcode                     |
| Flutter        | Dart                  | Android/iOS    | Multiplataforma  | Android Studio / VS Code |
| React Native   | JavaScript / TypeScript | Android/iOS    | Multiplataforma  | VS Code / Expo           |

---

## ✳️ Kotlin (Ênfase principal)

- 🟢 **Linguagem oficial do Android (Google)**
- ✅ 100% compatível com Java
- 🔒 Null safety
- ⚡ Sintaxe moderna e concisa
- 💡 Compatível com Jetpack Compose (nova UI declarativa)
- 📚 Ferramentas modernas: Coroutines, ViewModel, LiveData, Room, Retrofit

---

# 🧭 COMO FUNCIONA O DESENVOLVIMENTO DE UM APP

## 🧠 Backend (API)

Responsável pela **lógica de negócio** e **banco de dados**, muitas vezes feito em Node.js, Java (Spring), Python (Django), etc. O app mobile se comunica com ele via HTTP/HTTPS.

## 📱 Frontend Mobile (App)

Aplicativo instalado no celular, que consome a API para exibir dados ao usuário.

---

# 📘 README COMPLETO – DESENVOLVIMENTO MOBILE COM KOTLIN

## 📌 Objetivo

Este projeto é um ponto de partida para criar um app Android utilizando **Kotlin**, com arquitetura **MVVM**, persistência local com **Room**, comunicação com API usando **Retrofit** e uma interface criada com **XML** (ou **Jetpack Compose**).

---

## ⚙️ Requisitos

- ✅ Android Studio instalado  
- ✅ Kotlin configurado  
- ✅ Emululador ou dispositivo Android  
- ✅ JDK 11 ou superior  

---

## 📁 Estrutura de Pastas (MVVM)

```
MeuApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/exemplo/meuapp/
│   │   │   │   ├── model/         → Dados e entidades
│   │   │   │   ├── view/          → Activities/Fragments
│   │   │   │   ├── viewmodel/     → Regras de UI
│   │   │   │   ├── repository/    → Acesso a API ou banco
│   │   │   ├── res/
│   │   │   │   ├── layout/        → Telas XML
│   │   │   │   ├── values/        → strings.xml, colors.xml
│   │   │   │   ├── drawable/      → Imagens
│   │   │   ├── AndroidManifest.xml
├── build.gradle
└── settings.gradle
```

---

## 🧩 COMPONENTES ESSENCIAIS DO APP

| Componente        | Função |
|-------------------|--------|
| `Activity`        | Tela do app. Cada tela é uma Activity. |
| `Fragment`        | Subtela reutilizável dentro de uma Activity. |
| `ViewModel`       | Armazena e gerencia dados para UI. |
| `LiveData`        | Dados observáveis que reagem à mudança. |
| `RecyclerView`    | Lista dinâmica (ex: feed de posts). |
| `Room`            | Biblioteca para persistência local (banco de dados). |
| `Retrofit`        | Biblioteca para consumir APIs REST. |
| `Data Binding`    | Conecta dados diretamente com a UI. |
| `Jetpack Compose` | Alternativa moderna ao XML para construir UI com código Kotlin. |

---

## 🧠 CONCEITOS IMPORTANTES

### 1. Ciclo de Vida

Cada `Activity`/`Fragment` possui eventos como `onCreate`, `onStart`, `onPause`, etc. `ViewModel` ajuda a manter dados mesmo após rotação da tela.

### 2. Intents

Permitem navegação entre `Activities` ou interações com outros apps (abrir câmera, galeria, etc).

### 3. Permissões

Solicitadas no `AndroidManifest.xml` e em tempo de execução:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

### 4. Layout (XML) ou Compose

Define a interface com componentes como `Button`, `TextView`, `EditText`, etc.

---

## 📄 Arquivos Principais

| Arquivo                | Função                                 |
|------------------------|----------------------------------------|
| `MainActivity.kt`      | Tela inicial do app                    |
| `activity_main.xml`    | Layout visual da tela                  |
| `AndroidManifest.xml`  | Configura o app e permissões           |
| `build.gradle`         | Declara dependências e versões do app  |

---

## 🧪 Exemplo de Código Kotlin

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val botao = findViewById<Button>(R.id.botao)
        botao.setOnClickListener {
            Toast.makeText(this, "Olá, Sylvia!", Toast.LENGTH_SHORT).show()
        }
    }
}
```

---

## 🔌 Comunicação com API (Retrofit)

```kotlin
interface ApiService {
    @GET("usuarios")
    suspend fun getUsuarios(): List<Usuario>
}
```

---

## 🗄️ Banco de Dados Local (Room)

```kotlin
@Entity
data class Usuario(
    @PrimaryKey val id: Int,
    val nome: String
)

@Dao
interface UsuarioDao {
    @Query("SELECT * FROM Usuario")
    fun listar(): List<Usuario>
}
```

---

## 📦 Exemplo de dependências no `build.gradle`

```kotlin
dependencies {
    implementation "androidx.appcompat:appcompat:1.6.1"
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:2.6.1"
    implementation "androidx.recyclerview:recyclerview:1.3.1"
    implementation "androidx.room:room-runtime:2.6.1"
    kapt "androidx.room:room-compiler:2.6.1"
    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.1"
}
```

---

## 🧼 Boas Práticas

- ✅ Separar camadas (View, ViewModel, Model, Repository)
- ✅ Nunca fazer chamadas de rede direto na `Activity`
- ✅ Usar `ViewModel` + `LiveData` ou `StateFlow`
- ✅ Utilizar `Coroutines` para tarefas assíncronas
- ✅ Utilizar **Jetpack Libraries** para facilitar o desenvolvimento
