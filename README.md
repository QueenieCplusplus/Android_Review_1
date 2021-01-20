# Android_Review_1


Data Binding


1. create a new android project.

2. create a package, and assaign a name to it.

3. check dir called project/app/build.gradle, which are dependencies located. 

        3.1, check kotlin's version.
        3.2, check android sdk version is between 19~30.

4. create an empty Activity called MyName

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
            // ? means Nullable
            override fun onCreate(saveInstanceState: Bundle?){
               
               super.onCreate(saveInstanceState))
               
               binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
               
               binding.myName = myName
               
               // doneButton
               // related with UI elements
               binding.doneButton.setOnClickListener {
               
                  addNickname(it)
               
               }
            }
            
            // click handler
            private fun addNickname(view: View){
               
               //related with xml-formatted UI element
               binding.apply{
               
                 doneButton.visibility = View.GONE
                 nicknameEdit.visibility = View.GONE
                 nicknameText.visibitity = View.VISIBLE
                 
                 // input feature
                 // ? means Nullable
                 myName?.nickname = nicknameEdit.text.toString()
               
               }
            
            }
            
            // visible keyboard
            val imm = getSystemService(Context.INPUT_METHOD_SERVICE) as ImputMethodManager
            imm.hideSoftInputFromWindow(view.windowToken, 0)
        
        }
        
7. design layout in xml format.
   create a new layout called activity_main.xml which is reated to MainActivity.kt in src code.

        <?xml version="1.0" encoding="utf-8"?>

        <layout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:app="http://schemas.android.com/apk/res-auto">

            #Data bind with data class
            <data>
                <variable
                    name="myName"
                    type="com.example.android.katesapp.MyName" />
            </data>

            #A general-used layout style in Android.
            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical"
                android:paddingStart="@dimen/padding"
                android:paddingEnd="@dimen/padding">

                <TextView
                    android:id="@+id/name_text"
                    style="@style/NameStyle"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:text="@={myName.name}"
                    android:textAlignment="center" />

                <TextView
                    android:id="@+id/nickname_text"
                    style="@style/NameStyle"
                    android:text="@={myName.nickname}"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:textAlignment="center"
                    android:visibility="gone" />

                <EditText
                    android:id="@+id/nickname_edit"
                    style="@style/NameStyle"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:hint="@string/what_is_your_nickname"
                    android:inputType="textPersonName"
                    android:textAlignment="center" />

                <Button
                    android:id="@+id/done_button"
                    style="@style/Widget.AppCompat.Button.Colored"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center_horizontal"
                    android:layout_marginTop="@dimen/layout_margin"
                    android:fontFamily="@font/roboto"
                    android:text="@string/done"
                    android:textAlignment="center" />

                <ImageView
                    android:id="@+id/star_image"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="@dimen/layout_margin"
                    android:contentDescription="@string/yellow_star"
                    app:srcCompat="@android:drawable/btn_star_big_on" />

                <ScrollView
                    android:id="@+id/bio_scroll"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_marginTop="@dimen/layout_margin">

                    <TextView
                        android:id="@+id/bio_text"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:lineSpacingMultiplier="@dimen/line_spacing_multiplier"
                        android:text="@string/bio"
                        android:textAppearance="@style/NameStyle" />

                </ScrollView>
            </LinearLayout>
        </layout>


8. today's tip:

   https://medium.com/@louis383/kotlin-這些符號到底什麼意思-4274d3ae32ab
   
9. the relationship between UI ele & logical code. While using widget module instead of databiding.

       package com.android.example.katesapp
       
       import android.os.Bundle
       import androidx.appcompat.app.AppCompatActivity
       
       [add Interaction Module]
       import android.view.View
       import android.view.inputmethod.InputMethodMananger
       
       [add UI element module]
       [using widget instead of databinding]
       import android.widget.Button
       import android.widget.EditText
       import android.widget.TextView
       
       [keyboard]
       import android.content.Context
       
       class MainActivity : AppCompatActivity() {
       
           override fun onCreate(savedInstanceState: Bundle?){
           
                super.onCreate(savedInstanceState)
                
                setContentView(R.layout.activity_main)
                
                
                // Lifecycle Phase binding methods wait to be called.
                // 進入生命週期初始時，畫面便繫結 UI 元件的方法，等待觸動引發呼叫。
                
                // 編輯後
                findViewById<Button>(R.id.done_button).setOnClickListener {
                        inputHandler(it)
                }
           
                // 編輯前
                findViewById<TextView>(R.id.nickname_text).setOnClickListener{
                        btnHandler(it)
                }
           
           }
           
           
           // Special Effects
           // 方法經過畫面變動的參數，產生相應的特效結果。
           private fun inputHandler(view: View){
           
                val editor = findViewById<TextView>(R.id.nickname_edit)
                val viewer = findViewById<TextView>(R.id.nickname_text)
                
                // 編輯器的字串傳入畫面的字串顯示
                viewer.text = editor.text
                // 編輯器被隱藏
                editor.visibility = View.GONE
                // 編輯前的畫面被隱藏
                view.visibility = View.GONE
                // 編輯後的畫面被顯示
                viewer.visibility = View.VISIBLE
                
                // keyboard is hidden
                // Typecast 型別轉換，這而跟系統有關，不可以有 ? nullable
                val imm = getSystemService(Context.INPUT_METHOD_SERVICE) as InputMethodManager
                
                // 特效：鍵盤隱藏
                imm.hideSoftInputFromWindow(view.windowToken, 0)    
           
           }
           
           
           private fun visibleHandler(view: View){
           
                val editor = findViewById<EditText>(R.id.nickname_edit)
                val btn = findViewById<Button>(R.id.done_button)
                
                editor.visibility = View.VISIBLE
                btn.visibility = View.VISIBLE
                viewer.visibility = View.GONE
                
                // 特效：聚焦在編輯器上
                editor.requestFocus()
                
                // 特效：鍵盤顯示
                val imm = getSystemService(Context.INPUT_METHOD_SERVICE) as InputMehodManager
                imm.showSoftInput(editText, 0)
           
           }
       
       }

10. today's tip

    https://www.kotlincn.net/docs/reference/typecasts.html
