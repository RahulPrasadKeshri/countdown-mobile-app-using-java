# countdown mobile app
# here are the code to run the countdown mobile app using java
import android.os.Bundle;
import android.os.CountDownTimer;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class CountdownActivity extends AppCompatActivity {
    private TextView countdownText;
    private CountDownTimer countDownTimer;
    private long timeLeftInMillis; // Duration in milliseconds
    private static final long COUNTDOWN_INTERVAL = 1000; // Update interval in milliseconds

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_countdown);

        countdownText = findViewById(R.id.countdown_text);

        // Set the initial duration (e.g., 5 minutes = 5 * 60 * 1000 milliseconds)
        timeLeftInMillis = 5 * 60 * 1000;

        startCountdown();
    }

    private void startCountdown() {
        countDownTimer = new CountDownTimer(timeLeftInMillis, COUNTDOWN_INTERVAL) {
            @Override
            public void onTick(long millisUntilFinished) {
                timeLeftInMillis = millisUntilFinished;
                updateCountdownText();
            }

            @Override
            public void onFinish() {
                // Countdown has finished
                countdownText.setText("Countdown Complete");
            }
        }.start();
    }

    private void updateCountdownText() {
        int minutes = (int) (timeLeftInMillis / 1000) / 60;
        int seconds = (int) (timeLeftInMillis / 1000) % 60;

        String timeFormatted = String.format("%02d:%02d", minutes, seconds);
        countdownText.setText(timeFormatted);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (countDownTimer != null) {
            countDownTimer.cancel();
        }
    }
}
