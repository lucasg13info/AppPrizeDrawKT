package com.example.appprizedraw

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.input.nestedscroll.nestedScrollModifierNode
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.compose.runtime.getValue
import androidx.compose.runtime.setValue



class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            Home()
        }
    }
}



@Composable
fun Home(){
    val people = listOf(
        "Usher", "John", "Lucas", "Thadh", "Jack", "Pirer", "Carlo", "Edu", "Andre"
    )

    var vencedores by remember { mutableStateOf<List<String>>(emptyList()) }

    fun sorteio(){
        val sorteio = people.shuffled().take(3)
        vencedores = sorteio
    }

    Column (
        modifier = Modifier.fillMaxSize().background(Color.White),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "App Prize Draw",
            fontSize = 30.sp,
            fontWeight = FontWeight.Bold,
            modifier = Modifier.padding(50.dp)
        )
        Button(
            onClick = {
                sorteio()
            },
            colors = ButtonDefaults.buttonColors(
                contentColor = Color(0xFFFFFF)
            ),
            modifier = Modifier.padding(0.dp, 0.dp,0.dp, 20.dp)
        ) {
            Text(text = "Start",
                color = Color.White,
                fontSize = 18.sp,

            )
        }


        if (vencedores.isNotEmpty()) {
            vencedores.forEachIndexed { index, vencedor ->
                Text(
                    text = "Winner ${index + 1}: $vencedor",
                    fontSize = 15.sp,
                    fontWeight = FontWeight.Bold,
                    color = Color.Gray
                )
            }
        }

    }
}



@Preview
@Composable
private fun HomePreview(){
    Home()
}
