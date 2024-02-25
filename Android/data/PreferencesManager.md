```kotlin
private const val TAG = "PreferencesManager"

@Singleton
class PreferencesManager @Inject constructor(@ApplicationContext context: Context) {
    private val Context.dataStore: DataStore<Preferences> by preferencesDataStore(name = "preferences")
    private val dataStore = context.dataStore

    val example_id = dataStore.data
        .catch { exception ->
            if (exception is IOException) {
                Log.e(TAG, "Error reading preferences", exception)
                emit(emptyPreferences())
            } else {
                throw exception
            }
        }
        .map { preferences ->
            preferences[PreferenceKeys.DEVICE_ID] ?: ""
        }

    suspend fun updateExampleId(exampleId: String){
        dataStore.edit { preferences ->
            preferences[PreferenceKeys.EXAMPLE_ID] = exampleId
        }
    }
    

    private object PreferenceKeys {
        val EXAMPLE_ID = stringPreferencesKey("example_id")
    }
}
```