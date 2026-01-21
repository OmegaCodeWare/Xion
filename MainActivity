package com.omega.myproject

import android.content.res.Configuration
import android.net.Uri
import android.widget.VideoView
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.ui.unit.dp
import androidx.compose.ui.viewinterop.AndroidView
import androidx.compose.ui.draw.clip
import android.media.MediaPlayer
import androidx.compose.runtime.LaunchedEffect
import androidx.compose.runtime.mutableLongStateOf
import androidx.compose.material.LocalMinimumInteractiveComponentEnforcement



import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.animation.AnimatedVisibility
import androidx.compose.animation.fadeIn
import androidx.compose.animation.fadeOut
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.rememberScrollState
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.verticalScroll
import androidx.compose.material.ExperimentalMaterialApi
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.Slider
import androidx.compose.material3.SliderDefaults
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.CompositionLocalProvider
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clipToBounds
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.graphicsLayer
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.font.Font
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.compose.ui.viewinterop.AndroidView
import androidx.compose.ui.window.Dialog
import androidx.compose.ui.window.DialogProperties
import kotlinx.coroutines.delay
import androidx.compose.ui.platform.LocalConfiguration
import android.app.Activity
import android.content.pm.ActivityInfo
import androidx.compose.animation.core.tween
import androidx.compose.animation.slideInHorizontally
import androidx.compose.animation.slideOutHorizontally
import androidx.compose.runtime.saveable.rememberSaveable
import androidx.lifecycle.ViewModel
import androidx.navigation.NavController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController


class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        setContent {
            AppNavigation()
        }
    }
}

@Composable
fun AppNavigation() {
    val navController = rememberNavController()

    NavHost(
        navController = navController,
        startDestination = "main"
    ) {
        composable(
            route = "main",
            exitTransition = { fadeOut(tween(300)) }
        ) {
            MainContent(navController)
        }

        composable(
            route = "details",
            enterTransition = { slideInHorizontally(initialOffsetX = { it }) + fadeIn() },
            exitTransition = { slideOutHorizontally(targetOffsetX = { it }) + fadeOut() }
        ) {
            ChannelScreen(navController)
        }
    }
}


@Composable
fun MainContent(navController: NavController) {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .background(Color(0xFF1E1E1E))
            .verticalScroll(rememberScrollState())
    ) {
        Player()
        information()
        channel(navController)
        Comment()
        recom()
        recVideo()
        OpsVideo1()
        prevVideo2()
        opsVideo2()
        prevVideo3()
    }
}
@Composable
fun Player() {
    val context = LocalContext.current
    val activity = context as? Activity

    var isFullscreen by rememberSaveable { mutableStateOf(false) }
    var isPlaying by remember { mutableStateOf(true) }
    var isControlsVisible by remember { mutableStateOf(true) }
    var progress by remember { mutableStateOf(0f) }

    val videoView = remember {
        object : VideoView(context) {
            override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
                setMeasuredDimension(getDefaultSize(0, widthMeasureSpec), getDefaultSize(0, heightMeasureSpec))
            }
        }.apply {
            setVideoURI(Uri.parse("android.resource://${context.packageName}/raw/video"))
            setOnPreparedListener { mp ->
                mp.isLooping = true
                mp.setVideoScalingMode(MediaPlayer.VIDEO_SCALING_MODE_SCALE_TO_FIT_WITH_CROPPING)
                if (isPlaying) start()
            }
        }
    }

    LaunchedEffect(isPlaying) {
        while (isPlaying) {
            val duration = videoView.duration.toFloat()
            if (duration > 0) progress = videoView.currentPosition.toFloat() / duration
            delay(500)
        }
    }

    Box(
        modifier = if (isFullscreen) Modifier
            .fillMaxSize()
            .background(Color.Black)
        else Modifier
            .fillMaxWidth()
            .padding(start = 9.dp, end = 9.dp, top = 45.dp),
        contentAlignment = Alignment.Center
    ) {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(if (isFullscreen) 400.dp else 214.dp)
                .clip(RoundedCornerShape(if (isFullscreen) 0.dp else 24.dp))
                .background(Color.Black)
        ) {
            AndroidView(
                factory = { videoView },
                modifier = Modifier
                    .fillMaxSize()
                    .clipToBounds()
                    .clickable { isControlsVisible = !isControlsVisible }
            )

            AnimatedVisibility(visible = isControlsVisible, enter = fadeIn(), exit = fadeOut()) {
                Box(modifier = Modifier
                    .fillMaxSize()
                    .background(Color.Black.copy(0.2f))) {

                    IconButton(
                        onClick = {
                            if (isFullscreen) {
                                activity?.requestedOrientation = ActivityInfo.SCREEN_ORIENTATION_PORTRAIT
                                isFullscreen = false
                            } else {
                                isControlsVisible = false
                            }
                        },
                        modifier = Modifier
                            .align(Alignment.TopStart)
                            .padding(8.dp)
                    ) {
                        Icon(painter = painterResource(id = R.drawable.xmark), contentDescription = null, tint = Color.White, modifier = Modifier.size(15.dp))
                    }

                    IconButton(
                        onClick = { },
                        modifier = Modifier
                            .align(Alignment.TopEnd)
                            .padding(8.dp)
                    ) {
                        Icon(painter = painterResource(id = R.drawable.settings), contentDescription = null, tint = Color.White, modifier = Modifier.size(50.dp))
                    }

                    IconButton(
                        onClick = {
                            if (videoView.isPlaying) { videoView.pause(); isPlaying = false }
                            else { videoView.start(); isPlaying = true }
                        },
                        modifier = Modifier
                            .align(Alignment.Center)
                            .size(45.dp)
                    ) {
                        Icon(painter = painterResource(id = if (isPlaying) R.drawable.pause else R.drawable.play), contentDescription = null, tint = Color.White, modifier = Modifier.fillMaxSize())
                    }

                    Row(
                        modifier = Modifier
                            .fillMaxWidth()
                            .padding(horizontal = 16.dp, vertical = 24.dp)
                            .align(Alignment.BottomCenter),
                        verticalAlignment = Alignment.CenterVertically
                    ) {
                        Box(modifier = Modifier
                            .weight(1f)
                            .height(4.dp)
                            .background(Color.White.copy(0.3f))) {
                            Box(modifier = Modifier
                                .fillMaxWidth(progress)
                                .fillMaxHeight()
                                .background(Color.White))
                        }

                        Spacer(modifier = Modifier.width(12.dp))

                        IconButton(
                            onClick = {
                                if (isFullscreen) {
                                    activity?.requestedOrientation = ActivityInfo.SCREEN_ORIENTATION_PORTRAIT
                                    isFullscreen = false
                                } else {
                                    activity?.requestedOrientation = ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE
                                    isFullscreen = true
                                }
                            },
                            modifier = Modifier.size(25.dp)
                        ) {
                            Icon(painter = painterResource(id = R.drawable.fullscreen_enter), contentDescription = null, tint = Color.White, modifier = Modifier.fillMaxSize())
                        }
                    }
                }
            }
        }
    }

    LaunchedEffect(isControlsVisible, isPlaying) {
        if (isControlsVisible && isPlaying) {
            delay(3000)
            isControlsVisible = false
        }
    }
}

@Composable
fun opsVideo1 () {
    Row(modifier = Modifier
        .padding(top = 9.dp, start = 24.dp, end = 24.dp)
        .fillMaxWidth()
        .height(35.dp),
        horizontalArrangement = Arrangement.SpaceBetween,
        verticalAlignment = Alignment.CenterVertically
    ) {
        Column(

        ) {
            Text(text = "Introducing iPhone 16  ",
                color = Color(0xFFFFFFFF),
                fontSize = 16.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
            Row(
                horizontalArrangement = Arrangement.spacedBy(12.dp)
            ) {
                Text(text = "7,7 Mio. views",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
                Text(text = "5 months ago",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
            }

        }
        Box(
            modifier = Modifier
                .size(width = 88.dp, height = 28.dp)
                .background(
                    color = Color(0xFFB2B2B2)
                        .copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                ),
            contentAlignment = Alignment.Center
        ) {
            Text(text = "Watch",
                color = Color.White,
                fontSize = 13.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}
@Composable
fun information () {
    Column (
        modifier = Modifier.padding(top = 24.dp, start = 23.dp)
    ){
        Text(text = "Introducing iPhone 16 Pro ",
            color = Color.White,
            fontSize = 16.sp,
            fontFamily = FontFamily(
                Font(R.font.inter_regular)
            ))
        Row(
            modifier = Modifier.padding(top = 10.dp), horizontalArrangement = Arrangement.spacedBy(17.dp)
        ) {
            Text(text = "27 Mio. views",
                color = Color(0xFFB3B3B3),
                fontSize = 12.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)))

            Text(text = "5 months ago",
                color = Color(0xFFB3B3B3),
                fontSize = 12.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)))
        }
    }
}
@Composable
fun FollowButton() {
    var isFollowing by remember { mutableStateOf(false) }

    Box(
        modifier = Modifier
            .size(width = 88.dp, height = 28.dp)
            .background(
                color = if (!isFollowing) Color.White else Color(0xFFB2B2B2).copy(
                    alpha = if (isFollowing) 0.25f else 0.1f
                ),
                shape = RoundedCornerShape(20.dp)
            )
            .clickable { isFollowing = !isFollowing },
        contentAlignment = Alignment.Center
    ) {
        Text(
            text = if (isFollowing) "Following" else "Follow",
            color = if (isFollowing) Color.White else Color.Black,
            fontSize = 13.sp,
            fontFamily = FontFamily(Font(R.font.inter_regular))
        )
    }
}



@Composable
fun channel(navController: NavController) {
    Row(
        modifier = Modifier
            .padding(start = 23.dp, top = 12.dp, end = 23.dp)
            .fillMaxWidth(),
        horizontalArrangement = Arrangement.SpaceBetween,
        verticalAlignment = Alignment.CenterVertically
    ) {
        Row(
            horizontalArrangement = Arrangement.spacedBy(7.dp),
            verticalAlignment = Alignment.CenterVertically,
            modifier = Modifier
                .clickable {
                    navController.navigate("details")
                }
                .padding(4.dp)
        ) {
            Image(
                painter = painterResource(R.drawable.image1),
                contentDescription = "Logo",
                modifier = Modifier.size(30.dp)
            )

            Text(
                text = "Apple",
                color = Color.White,
                fontSize = 14.sp,
                fontFamily = FontFamily(Font(R.font.inter_regular))
            )
        }
        FollowButton()
    }
}

@Composable
fun Comment() {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .height(80.dp)
            .padding(start = 22.dp, end = 22.dp, top = 21.dp)
            .background(
                color = Color(0xFFB2B2B2).copy(alpha = 0.1f),
                shape = RoundedCornerShape(15.dp)
            ),
        verticalArrangement = Arrangement.SpaceEvenly
    ) {
        Row(
            horizontalArrangement = Arrangement.spacedBy(5.dp),
            verticalAlignment = Alignment.CenterVertically,
            modifier = Modifier.padding(start = 11.dp)
        ) {
            Image(
                painter = painterResource(R.drawable.rectangle5),
                contentDescription = "Logo",
                modifier = Modifier.size(20.dp)
            )
            Text(text = "Tim Apple",
                color = Color(0xFFFFFFFF),
                fontSize = 12.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
        Text(text = "It’s the best iPhone ever made",
            color = Color(0xFFFFFFFF),
            fontSize = 12.sp,
            fontFamily = FontFamily(
                Font(R.font.inter_regular)
            ),
            modifier = Modifier.padding(start = 11.dp)
        )
    }
}

@Composable
fun recom () {
    Text(text = "More like this",
        color = Color(0xFFFFFFFF),
        fontSize = 16.sp,
        fontFamily = FontFamily(
            Font(R.font.inter_regular)
        ),
        modifier = Modifier.padding(start = 24.dp, top = 22.dp)
    )
}

@Composable
fun recVideo () {
    Box(
        modifier = Modifier
            .padding(start = 23.dp, end = 23.dp, top = 12.dp)
            .fillMaxWidth()
            .height(163.dp)
    ){
        Image(
            painter = painterResource(R.drawable.image2),
            contentDescription = "video",
            contentScale = ContentScale.Crop,
            modifier = Modifier.fillMaxSize()
        )

        Row(
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.spacedBy(7.dp),
            modifier = Modifier
                .padding(start = 7.dp, top = 8.dp)
                .align(Alignment.TopStart)
                .size(width = 95.dp, height = 36.dp)
                .background(
                    color = Color(0xFFB2B2B2).copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                )
        ){
            Image(
                painter = painterResource(R.drawable.image6),
                contentDescription = "Logo",
                modifier = Modifier.size(30.dp)
            )

            Text(text = "Apple",
                color = Color(0xFFFFFFFF),
                fontSize = 14.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}

@Composable
fun OpsVideo1 () {
    Row(modifier = Modifier
        .padding(top = 9.dp, start = 24.dp, end = 24.dp)
        .fillMaxWidth()
        .height(35.dp),
        horizontalArrangement = Arrangement.SpaceBetween,
        verticalAlignment = Alignment.CenterVertically
    ) {
        Column(

        ) {
            Text(text = "Introducing iPhone 16  ",
                color = Color(0xFFFFFFFF),
                fontSize = 16.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
            Row(
                horizontalArrangement = Arrangement.spacedBy(12.dp)
            ) {
                Text(text = "7,7 Mio. views",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
                Text(text = "5 months ago",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
            }

        }
        Box(
            modifier = Modifier
                .size(width = 88.dp, height = 28.dp)
                .background(
                    color = Color(0xFFB2B2B2)
                        .copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                ),
            contentAlignment = Alignment.Center
        ) {
            Text(text = "Watch",
                color = Color.White,
                fontSize = 13.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}
@Composable
fun prevVideo2 () {
    Box(
        modifier = Modifier
            .padding(start = 24.dp, end = 24.dp, top = 20.dp)
            .fillMaxSize()
    ){
        Image(
            painter = painterResource(R.drawable.hq720),
            contentDescription = "video",
            contentScale = ContentScale.Crop,
            modifier = Modifier.fillMaxSize()
        )

        Row(
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.spacedBy(7.dp),
            modifier = Modifier
                .padding(start = 7.dp, top = 8.dp)
                .align(Alignment.TopStart)
                .size(width = 95.dp, height = 36.dp)
                .background(
                    color = Color(0xFFB2B2B2).copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                )
        ){
            Image(
                painter = painterResource(R.drawable.image6),
                contentDescription = "Logo",
                modifier = Modifier.size(30.dp)
            )

            Text(text = "Apple",
                color = Color(0xFFFFFFFF),
                fontSize = 14.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}

@Composable
fun opsVideo2 () {
    Row(modifier = Modifier
        .padding(top = 9.dp, start = 24.dp, end = 24.dp)
        .fillMaxWidth()
        .height(35.dp),
        horizontalArrangement = Arrangement.SpaceBetween,
        verticalAlignment = Alignment.CenterVertically
    ) {
        Column(

        ) {
            Text(text = "Introducing iPhone 17   ",
                color = Color(0xFFFFFFFF),
                fontSize = 16.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
            Row(
                horizontalArrangement = Arrangement.spacedBy(12.dp)
            ) {
                Text(text = "21 Mio. views",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
                Text(text = "3 months ago",
                    color = Color(0xFFB3B3B3),
                    fontSize = 12.sp,
                    fontFamily = FontFamily(
                        Font(R.font.inter_regular)
                    ))
            }

        }
        Box(
            modifier = Modifier
                .size(width = 88.dp, height = 28.dp)
                .background(
                    color = Color(0xFFB2B2B2)
                        .copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                ),
            contentAlignment = Alignment.Center
        ) {
            Text(text = "Watch",
                color = Color.White,
                fontSize = 13.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}

@Composable
fun prevVideo3 () {
    Box(
        modifier = Modifier
            .padding(start = 24.dp, end = 24.dp, top = 20.dp)
            .fillMaxSize()
    ){
        Image(
            painter = painterResource(R.drawable.image),
            contentDescription = "video",
            contentScale = ContentScale.Crop,
            modifier = Modifier.fillMaxSize()
        )

        Row(
            verticalAlignment = Alignment.CenterVertically,
            horizontalArrangement = Arrangement.spacedBy(7.dp),
            modifier = Modifier
                .padding(start = 7.dp, top = 8.dp)
                .align(Alignment.TopStart)
                .size(width = 95.dp, height = 36.dp)
                .background(
                    color = Color(0xFFB2B2B2).copy(alpha = 0.1f),
                    shape = RoundedCornerShape(50.dp)
                )
        ){
            Image(
                painter = painterResource(R.drawable.image6),
                contentDescription = "Logo",
                modifier = Modifier.size(30.dp)
            )

            Text(text = "Apple",
                color = Color(0xFFFFFFFF),
                fontSize = 14.sp,
                fontFamily = FontFamily(
                    Font(R.font.inter_regular)
                ))
        }
    }
}
