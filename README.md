# Android_Review_1
Data Binding


1. create a new android project.

2. create a package, and assaign a name to it.

3. check dir called project/app/build.gradle, which are dependencies located. 
   3.1, check kotlin's version.
   3.2, check android sdk version is between 19~30.

4. ceate an empty Activity.

        package com.example.android.katesapp


        import android.os.Bundle
        import androidx.appcompat.app.AppCompatActivity

        class MainActivity: AppCompatActivity(){
        
           override fun onCreate(savedInstanceState: Bundle?){
           
              super.onCreate(savedInstanceState)
              setContentView(R.layout.activity_main)
              
           }
        
        }
       

5. create a data class.


        package com.example.android.katesapp

        data class MyName(var name: String = "", var nickname: String = "")
        
6. instead of making Activity to import Data class, we can import databinding modules.

        package com.example.android.katesapp
        
        [remain the following modules]
        
        import android.os.Bundle
        import androidx.appcompat.app.AppCompatActivity
        
        [add the following modules]
        import com.example.android.katesapp.databinding.ActivityMainBinding
        imoort androidx.databinding.DataBindingUtil
        
        
        
        
