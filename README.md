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
        
        [add the following modules to do data bind]
        import com.example.android.katesapp.databinding.ActivityMainBinding
        imoort androidx.databinding.DataBindingUtil
        
        [add the following modules to do input feature]
        import android.view.View
        import andoroid.view.imputmethod.InputMethodManager
        
        class MainActivity: AppCompatActivity(){
        
            //data bind
            private lateinit var binding: ActivityMainBinding
            
            // immutable & as Final Var
            // using Dtata Class called MyName(param1, param2), param as optional
            priavte val myName: MyName = MyName("Kate Chen")
            
            
            // LifeCycle in Andorid System
            // local var
            override fun onCreate(saveInstanceState: Bundle?){
               
               super.onCreate(saveInstanceState))
               
               binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
               
               binding.myName = myName
               
               // doneButton
               binding.doneButton.setOnClickListener {
               
                  addNickname(it)
               
               }
            }
            
            // click handler
            private fun addNickname(view: View){
               
               binding.apply{ //omit}
            
            }
            
            // visible keyboard
            val imm = getSystemService(Context.INPUT_METHOD_SERVICE) as ImputMethodManager
            imm.hideSoftInputFromWindow(view.windowToken, 0)
        
        }
        
        
        
        
