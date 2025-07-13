# Friendly-FAQ-Chatbot-App
**Step 1:** Project Setup
Tools:
- Android Studio with Kotlin
- Jetpack Compose enabled
Create a new project:
- Template: Empty Compose Activity
- Name: BasicFaqChatbot
- Minimum SDK: API 21+
Add dependencies to build.gradle:

Code:
Groovy
implementation "androidx.compose.ui:ui:1.6.0"
implementation "androidx.navigation:navigation-compose:2.7.0"

**Step 2:** Define Data Model
Create a simple model to represent FAQs grouped by tags.
Kotlin
data class FAQ(
    val keyword: String,
    val question: String,
    val answer: String
)

**Step 3:** Create Static FAQ Dataset
You’ll use a Kotlin list or map to store predefined FAQs:
Kotlin
val faqData = listOf(
    FAQ("Returns", "Can I return a product?", "Yes, returns are accepted within 7 days."),
    FAQ("Pricing", "Is tax included?", "Prices are inclusive of GST."),
    FAQ("Availability", "Is this product in stock?", "Stock varies by location. Check availability online.")
)

Or for keyword grouping:
Kotlin
val faqMap = mapOf(
    "Returns" to listOf("Can I return a product?" to "Yes, returns are accepted within 7 days."),
    "Pricing" to listOf("Is tax included?" to "Prices are inclusive of GST.")
)

💬 Step 4: Chat UI with Jetpack Compose
Create a layout that mimics basic chat:
Kotlin
@Composable
fun FAQChatScreen() {
    var userQuery by remember { mutableStateOf("") }
    var botResponse by remember { mutableStateOf("") }

    Column(modifier = Modifier.padding(16.dp)) {
        TextField(
            value = userQuery,
            onValueChange = { userQuery = it },
            label = { Text("Ask your question") }
        )

        Spacer(modifier = Modifier.height(8.dp))

        Button(onClick = {
            botResponse = matchFAQ(userQuery)
        }) {
            Text("Submit")
        }

        Spacer(modifier = Modifier.height(16.dp))
        Text("Bot Response: $botResponse")
    }
}

🔎 Step 5: Matching Logic for FAQs
Implement simple keyword or substring matching:
Kotlin
fun matchFAQ(query: String): String {
    val lowerQuery = query.lowercase()
    for (faq in faqData) {
        if (lowerQuery.contains(faq.keyword.lowercase()) ||
            lowerQuery.contains(faq.question.lowercase())) {
            return faq.answer
        }
    }
    return "Sorry, I don't have an answer for that yet."
}

🌟 Step 6: Prepare for Azure OpenAI Upgrade
You can later replace matchFAQ() with an API call to an Azure-hosted GPT endpoint.
Retrofit Interface (for future AI step):
Kotlin
interface GPTService {
    @POST("getAnswer")
    suspend fun getAnswer(@Body question: String): GPTResponse
}

Azure Function Tips:
- Use Firebase Auth or headers for security
- Store GPT credentials in Azure Key Vault

🎨 Optional Enhancements
- Add FAQ suggestion buttons (“Returns”, “Pricing”) for faster queries
- Display history of Q&A in chat bubbles
- Color differentiation: user vs bot messages
- Save responses offline using Room or DataStore
**
Would you like a wireframe diagram or JSON mockup for the FAQ dataset next? We can even layer in Compose animations or iconography later. **

Detailed steps for Step 1:
Step 1: Project Setup in Android Studio (Kotlin + Jetpack Compose)
✅ 1. Open Android Studio
- Launch Android Studio (latest stable version recommended)
- Click on “New Project”

✅ 2. Choose Project Template
- Select “Empty Compose Activity”
- This sets up a basic Jetpack Compose-compatible activity
- Click Next

✅ 3. Configure Project Details
- Name: BasicFaqChatbot
- Package Name: com.yourname.basicfaqchatbot
- Language: Kotlin
Absolutely, Isha! Let’s walk through Step 1 of your FAQ Chatbot App implementation in Android Studio, using Kotlin and Jetpack Compose. This phase covers creating a fresh project with all the required settings and dependencies—crystal clear and beginner-friendly.

🛠️ Step 1: Project Setup in Android Studio (Kotlin + Jetpack Compose)
✅ 1. Open Android Studio
- Launch Android Studio (latest stable version recommended)
- Click on “New Project”

✅ 2. Choose Project Template
- Select “Empty Compose Activity”
- This sets up a basic Jetpack Compose-compatible activity
- Click Next

✅ 3. Configure Project Details
- Name: BasicFaqChatbot
- Package Name: com.yourname.basicfaqchatbot
- Language: Kotlin
- Minimum API Level: API 21 or higher (recommend API 24+ for Compose compatibility)
- Click Finish to generate the starter code.

✅ 4. Enable Firebase (Optional for Later Use)
You can set this up now or in Step 3 when Firestore is needed.
- Go to Firebase Console
- Create a Firebase project
- In Android Studio: open Tools > Firebase
- Use the Assistant to connect your app and download google-services.json
- Place google-services.json in your app’s /app directory

5. Update Gradle Files
Edit these two files to include necessary dependencies:
build.gradle (project)
Make sure this includes:
Groovy:
classpath 'com.google.gms:google-services:4.3.15' // for Firebase

build.gradle (app)
Add Jetpack Compose and Firebase Firestore dependencies:

Groovy
android {
    ...
    buildFeatures {
        compose true
    }
    composeOptions {
        kotlinCompilerExtensionVersion '1.6.0'
    }
}

dependencies {
    // Jetpack Compose
    implementation "androidx.compose.ui:ui:1.6.0"
    implementation "androidx.navigation:navigation-compose:2.7.0"
    implementation "androidx.compose.material:material:1.6.0"

    // Firebase Firestore (Optional)
    implementation 'com.google.firebase:firebase-firestore-ktx:24.10.0'

    // For future GPT API integration
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
}

apply plugin: 'com.google.gms.google-services'  // Firebase plugin

Sync your project when prompted.

✅ 6. Run the App
- Open MainActivity.kt
- Replace the default UI with a simple Compose preview:

Kotlin
@Composable
fun GreetingScreen() {
    Text("Welcome to FAQ Chatbot", style = MaterialTheme.typography.h5)
}

@Preview(showBackground = true)
@Composable
fun PreviewGreeting() {
    GreetingScreen()
}

- Hit Run to make sure everything launches correctly on emulator or device.







