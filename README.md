# Guftgo

### Hi there,  <img src="https://github.com/TheDudeThatCode/TheDudeThatCode/blob/master/Assets/Hi.gif" width="29px">

[![Website](https://img.shields.io/website?label=kant146.wordpress.com&style=for-the-badge&url=https%3A%2F%2Fkant146.wordpress.com)](https://kant146.wordpress.com)
[![Instagram Badge](https://img.shields.io/badge/-instagram-red?style=for-the-badge&logo=instagram&logoColor=white&link=https://www.instagram.com/kant_146/)](https://www.instagram.com/kant_146/)&nbsp;
<a href="mailto:krishnakantkumar146@gmail.com"><img src="https://www.flaticon.com/svg/static/icons/svg/646/646187.svg" width="30" height="30"></a>


## I am krishnakant !! 

 here trying give you my best , appreciate my work.

This is a video Calling  Android Application in Java.

Guftgu is free and useful messaging , chatting, meeting, streaming, watching and listening app with your friends and family or many more uses. Get access to the world and connect to your friends with the brand new mesenger app.


App download link

https://lnkd.in/g3-5PWu

Create room and call everyone

### Connect with me:

[![Linkedin Badge](https://img.shields.io/badge/-linkedn-blue?style=for-the-badge&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/krishnakant-kumar-80965b176/)](https://www.linkedin.com/in/krishnakant-kumar-80965b176/)&nbsp;[![Instagram Badge](https://img.shields.io/badge/-instagram-8a3ab9?style=for-the-badge&logo=instagram&logoColor=white&link=https://www.instagram.com/kant_146/)](https://www.instagram.com/kant_146/)&nbsp;[![Hashnode Badge](https://img.shields.io/badge/-hashnode-2962FF?style=for-the-badge&logo=hashnode&logoColor=white&link=https://hashnode.com/@Kant146)](https://hashnode.com/@Kant146)&nbsp;
<br/>[![Medium Badge](https://img.shields.io/badge/-medium-000000?style=for-the-badge&logo=medium&logoColor=white&link=https://medium.com/@krishnakantkumar_32146)](https://medium.com/@krishnakantkumar_32146)&nbsp; [![Youtube Badge](https://img.shields.io/badge/-youtube-FF0000?style=for-the-badge&logo=youtube&logoColor=white&link=https://www.youtube.com/channel/UCBTwzxjvK-0gGuJ1g_LlP8Q)](https://www.youtube.com/channel/UCBTwzxjvK-0gGuJ1g_LlP8Q)&nbsp; [![Facebook Badge](https://img.shields.io/badge/-facebook-blue?style=for-the-badge&logo=facebook&logoColor=white&link=https://www.facebook.com/omgkant.146)](https://www.facebook.com/omgkant.146)&nbsp; 



![Webp net-resizeimage](https://user-images.githubusercontent.com/47590877/111044054-4726ed80-846c-11eb-974c-027a70058bbd.jpg)
![Webp net-resizeimage (1)](https://user-images.githubusercontent.com/47590877/111044119-a422a380-846c-11eb-897a-294de19d1aa3.jpg)
![Webp net-resizeimage (2)](https://user-images.githubusercontent.com/47590877/111044182-09769480-846d-11eb-8625-eb19bace4172.jpg)
![Webp net-resizeimage (3)](https://user-images.githubusercontent.com/47590877/111044218-3aef6000-846d-11eb-982a-825e8b3697e9.jpg)
![Webp net-resizeimage (4)](https://user-images.githubusercontent.com/47590877/111044457-eb119880-846e-11eb-927d-79be614c51da.jpg)




some usefull elements 

1. LoginActivity

package com.example.guftgo;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.app.ProgressDialog;
import android.content.Intent;
import android.os.Bundle;
import android.text.Editable;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class LoginActivity extends AppCompatActivity {

    EditText emailBox, passwordBox;
    Button loginBtn, signupBtn;

    FirebaseAuth auth;

    ProgressDialog dialog;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_login);

        dialog = new ProgressDialog(this);
        dialog.setMessage("Please wait...");

        auth = FirebaseAuth.getInstance();

        emailBox = findViewById(R.id.emailBox);
        passwordBox = findViewById(R.id.passwordBox);

        loginBtn = findViewById(R.id.loginbtn);
        signupBtn = findViewById(R. id.createbtn);


        loginBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                dialog.show();
                String email, password;
                email = emailBox.getText().toString();
                password = passwordBox.getText().toString();

                auth.signInWithEmailAndPassword(email, password).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        dialog.dismiss();
                        if (task.isSuccessful())
                        {
                            startActivity(new Intent(LoginActivity.this, DashboardActivity.class));
                        } else {
                            Toast.makeText(LoginActivity.this, task.getException().getLocalizedMessage(), Toast.LENGTH_SHORT).show();
                        }
                    }
                });
            }
        });

        signupBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                startActivity(new Intent(LoginActivity.this, SignupActivity.class));
            }
        });

    }
}


2.SignupActivity
package com.example.guftgo;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.firestore.FirebaseFirestore;

public class SignupActivity extends AppCompatActivity {

    FirebaseAuth auth;
    EditText emailBox, passwordBox, nameBox;
    Button loginBtn, signupBtn;

    FirebaseFirestore database;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_signup);

        database = FirebaseFirestore.getInstance();
        auth = FirebaseAuth.getInstance();

        emailBox = findViewById(R.id.emailBox);
        nameBox = findViewById(R.id.namebox);
        passwordBox = findViewById(R.id.passwordBox);

        loginBtn = findViewById(R.id.loginbtn);
        signupBtn = findViewById(R. id.createbtn);

        signupBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String email, pass, name;
                email = emailBox.getText().toString();
                pass = passwordBox.getText().toString();
                name = nameBox.getText().toString();

                User user = new User();
                user.setEmail(email);
                user.setPass(pass);
                user.setName(name);

                auth.createUserWithEmailAndPassword(email, pass).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if (task.isSuccessful()) {
                            database.collection("Users")
                                    .document().set(user).addOnSuccessListener(new OnSuccessListener<Void>() {
                                @Override
                                public void onSuccess(Void aVoid) {
                                    startActivity(new Intent(SignupActivity.this, LoginActivity.class));
                                }
                            });
                            Toast.makeText(SignupActivity.this,  "Account is created", Toast.LENGTH_SHORT).show();
                        } else {
                            Toast.makeText(SignupActivity.this, task.getException().getLocalizedMessage(), Toast.LENGTH_SHORT).show();
                        }
                    }
                });

            }
        });
    }
}
