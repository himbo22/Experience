#Create Modules

```kotlin
@Module
@InstallIn(SingletonComponent::class)
class AppModule {

    @Provides
    fun provideDatabase(
        app: Application,
        callback: UserDatabase.Callback
    ) = Room.databaseBuilder(app, UserDatabase::class.java, "user_database")
        .fallbackToDestructiveMigration()
        .addCallback(callback)
        .build()

    @Provides
    fun provideTaskDao(db: UserDatabase) = db.userDao()

    @ApplicationScope
    @Provides
    fun provideApplicationScope() = CoroutineScope(SupervisorJob())

    @Provides
    fun provideRetrofit(client: OkHttpClient): Retrofit = Retrofit.Builder()
        .addConverterFactory(GsonConverterFactory.create())
        .client(client)
        .baseUrl("https://mionix.ddns.net/soundscapeapi/")
        .build()

    @Provides
    fun provideAuthInterceptor() = AuthInterceptor()

    @Provides
    fun provideSignInRepository(apiService: ApiService): SignInRepository =
        SignInRepositoryImp(apiService)

    @Provides
    fun provideHttpClient(
        authInterceptor: AuthInterceptor,
    ) = OkHttpClient.Builder().run {
        addInterceptor(authInterceptor)
        if (BuildConfig.DEBUG) {
            addInterceptor(HttpLoggingInterceptor().apply {
                level = HttpLoggingInterceptor.Level.BODY
            })
        }
        build()
    }

    @Provides
    fun provideApiService(retrofit: Retrofit): ApiService = retrofit.create(ApiService::class.java)
}
```

## Annotate @Module and @InstallIn(SingletonComponent::class) 

If we want to create modules by dependencies injection then both of annotates must be contained in the Module Class.
