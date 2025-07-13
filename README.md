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

Would you like a wireframe diagram or JSON mockup for the FAQ dataset next? We can even layer in Compose animations or iconography later. 





