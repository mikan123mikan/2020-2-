使用言語はJavaです。アンドロイドで遊べるホッケーのゲームで、3段階の強さを持ったコンピューターと
対戦することができます。

    public class MainActivity extends AppCompatActivity {
    CustomView cv;
    SensorManager sm;
    SEL sel;
    float[] a_vals = new float[3];
    MediaPlayer mp1;   //はじいた時の効果音を付けています
    int ff = 0;
    int j = 0;
    int qq = 0;
    int touch2 = 0;
    int kati12 = 0;
    int kati11 = 0;
    int myrak = 0;
    int katihuragu = 0;
    int b1my = 0, b2my = 0, b3my = 0, b1cp = 0, b2cp = 0, b3cp = 0;
    int makehuragu = 0;
    int cpuk = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        MyView mv = new MyView(this);
        setContentView(mv);
        this.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
        cv = new CustomView(this);
        AnimationDrawable anim = new AnimationDrawable();
        anim.setOneShot(true);
        ViewCompat.setBackground(mv, anim);
        anim.start();
        mp1 = MediaPlayer.create(this, R.raw.hannsha);
    }

    public void onResume() {
        super.onResume();
        sm = (SensorManager) getSystemService(Context.SENSOR_SERVICE);     //スマホに内蔵されたセンサーを使います
        Sensor se = sm.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);       //加速度
        sel = new SEL();
        sm.registerListener(sel, se, SensorManager.SENSOR_DELAY_FASTEST);  //遅延が一番少ないものを選びます
    }
    protected void onPause() {
        super.onPause();
        sm.unregisterListener(sel);
    }


    class MyView extends View {
        Paint pa = new Paint();
        Paint pa2 = new Paint();
        Paint pa3 = new Paint();
        int x = 300, y = 300, y2 = 300, y3 = 300, col = Color.BLUE;
        int x2 = 500, x3 = 700;
        int q = 0, q2 = 0, q3 = 0, w = 0, w2 = 0, w3 = 0;
        float c = 0;
        int s = 484, d = 584, f = 1520, g = 1540;           //ラケットの初期位置を設定しています
        int k = 2;
        int a = 0;
        int cpux = 0;
        int cpuraa = 0;
        int cpupo = 0, mypo = 0;
        int myrak2 = 0;
        int kati1 = 0, kati2 = 0;
        float yyy = 0;

        public MyView(Context context) {
            super(context);
        }

        protected void onDraw(Canvas ca) {
            super.onDraw(ca);
            pa.setColor(col);
            pa3.setColor(Color.BLACK);
            yyy = ca.getHeight();
            Rect r = new Rect();

            ca.drawRect(c + s, yyy - 20, c + d, yyy, pa);       //ラケットを描画しています

            Rect cpu = new Rect();
            cpu.set(ca.getWidth() / 2 - 50 + cpux, 0, ca.getWidth() / 2 + 50 + cpux, 20);
            pa2.setColor(RED);
            ca.drawRect(cpu, pa2);          //敵ラケットです

            int cpurrrr = (int) (Math.random() * 20 - cpuk);        //敵のラケットが次に動く範囲をランダムで出しています

            int cpura = (int) ((Math.random() * ca.getWidth()) - ca.getWidth() / 2);
            if (w == 1 && y < ca.getHeight() / 3 && y > 0) {
                if (cpurrrr == 0) {
                    cpux = ca.getWidth() / 2 * (-1) + x;
                } else if (cpuraa == 25) {
                    cpux = cpura;
                    cpuraa = 0;
                }
                if (cpuk == 18 && (cpuraa % 12 == 2)) {         //敵の動作を安定させています(動きすぎないようにカウンタで制御)
                    if (q == 0) {
                        cpux = ca.getWidth() / 2 * (-1) + x;        //乱数が良い値の時だけ敵ラケットがボールの座標に移動します。
                    } else {
                        cpux = ca.getWidth() / 2 * (-1) + x;
                    }
                }
                if (cpuk == 19 && (cpuraa % 7 == 2)) {
                    if (q == 0) {
                        cpux = ca.getWidth() / 2 * (-1) + x;
                    } else {
                        cpux = x - 12;
                    }
                }
                cpuraa++;
            } else if (w2 == 1 && y2 < ca.getHeight() / 3 && y2 > 0) {
                if (cpurrrr == 0) {
                    cpux = ca.getWidth() / 2 * (-1) + x2;
                } else {
                    if (cpuraa == 25) {
                        cpux = cpura;
                        cpuraa = 0;
                    } else {
                        if (cpuk == 18 && (cpuraa % 12 == 2)) {
                            if (q2 == 0) {
                                cpux = ca.getWidth() / 2 * (-1) + x2;
                            } else {
                                cpux = ca.getWidth() / 2 * (-1) + x2;
                            }
                        }
                        if (cpuk == 19 && (cpuraa % 4 == 2)) {
                            if (q2 == 0) {
                                cpux = ca.getWidth() / 2 * (-1) + x2;
                            } else {
                                cpux = ca.getWidth() / 2 * (-1) + x2;
                            }
                        }
                        cpuraa++;
                    }
                }
            } else if (w3 == 1 && y3 < ca.getHeight() / 3 && y3 > 0) {
                if (cpurrrr == 0) {
                    cpux = ca.getWidth() / 2 * (-1) + x3;
                } else {
                    if (cpuraa == 25) {
                        cpux = cpura;
                        cpuraa = 0;
                    } else {
                        if (cpuk == 18 && (cpuraa % 12 == 2)) {
                            if (q3 == 0) {
                                cpux = ca.getWidth() / 2 * (-1) + x3;
                            } else {
                                cpux = ca.getWidth() / 2 * (-1) + x3;
                            }
                        }
                        if (cpuk == 19 && (cpuraa % 4 == 2)) {
                            if (q3 == 0) {
                                cpux = ca.getWidth() / 2 * (-1) + x3;
                            } else {
                                cpux = ca.getWidth() / 2 * (-1) + x3;
                            }
                        }
                        cpuraa++;
                    }
                }
            } else if (cpuraa == 25) {
                if (cpux - cpura <= ca.getWidth() / 3 && cpux - cpura >= ca.getWidth() / 3 * (-1)) {
                    cpux = cpura;
                    cpuraa = 0;
                }
            } else {
                cpuraa = cpuraa + 1;
            }

            ca.drawCircle(x, y, 30, pa);        //ボールです。最大3個同時に動きます。
            ca.drawCircle(x2, y2, 30, pa);
            ca.drawCircle(x3, y3, 30, pa);

            if (katihuragu == 0) {          //コンピューターと戦っている間の処理
                if (touch2 >= 1) {
                    if (q == 0 && w == 0) {     //qとwはボールが移動する左右上下の向きです。
                        x = x + 5 + k;
                        if (x > ca.getWidth())
                            q = 1;          //画面の横端では反射させます。上下ではラケットに当たった時だけ反射させます。
                        y = y + 5 + k;
                        if (y > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = cpupo + 1;      //コンピューターが1ポイント獲得した時の処理
                            }
                            b1cp = 1;
                            myrak = 1;
                        }

                    }
                    if (q == 1 && w == 0) {
                        x = x - 5 - k;
                        if (x < 0)
                            q = 0;
                        y = y + 5 + k;
                        if (y > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = 1;
                            }
                            b1cp = 1;
                            myrak = 1;
                        }
                    }

                    if (a_vals[0] < -0.5 || a_vals[0] > 0.5) {
                        c = (c - (a_vals[0]) * 5);
                    }
                    if (c + s < 0) c = -s;
                    if (c + d > ca.getWidth()) c = ca.getWidth() - d;
                    if ((s + c) < x && x < (c + d) && y > ca.getHeight() - 20 && y < ca.getHeight()) {
                        myrak = 1;
                        try {
                            mp1.prepare();
                        } catch (Exception e) {
                            e.printStackTrace();          //動作を安定させています
                        }
                        if (mp1.isPlaying()) {
                            mp1.seekTo(0);
                        }
                        mp1.start();
                        if (q == 0 && w == 0) {
                            w = 1;
                        }
                        if (q == 1 && w == 0) {
                            w = 1;
                        }
                    }
                    if (q == 1 && w == 1) {
                        x = x - 5 - k;
                        if (x < 0) {
                            q = 0;
                            w = 1;
                        }
                        y = y - 5 - k;
                        if (y < 20 && y > 0 && x < ca.getWidth() / 2 + 50 + cpux && x > ca.getWidth() / 2 - 50 + cpux) {
                            q = 1;
                            w = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y < 0) {
                            if (mypo == 0) {
                                mypo = 1;
                            }
                            b1my = 1;
                        }
                    }
                    if (q == 0 && w == 1) {
                        x = x + 5 + k;
                        if (x > ca.getWidth()) {
                            q = 1;
                            w = 1;
                        }
                        y = y - 5 - k;
                        if (y < 20 && y > 0 && x < ca.getWidth() / 2 + 50 + cpux && x > ca.getWidth() / 2 - 50 + cpux) {
                            q = 0;
                            w = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y < 0) {
                            if (mypo == 0) {
                                mypo = 1;
                            }
                            b1my = 1;
                        }
                    }
                }
                if (myrak == 1) {               //myrakという変数で、1個めのボールを弾いたことを確認し、2個めのボールを動かしだします。
                    if (q2 == 0 && w2 == 0) {
                        x2 = x2 + 5 + k;
                        if (x2 > ca.getWidth())
                            q2 = 1;
                        y2 = y2 + 5 + k;
                        if (y2 > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = 1;
                            }
                            b2cp = 1;
                            myrak2 = 1;
                        }
                    }
                    if (q2 == 1 && w2 == 0) {
                        x2 = x2 - 5 - k;
                        if (x2 < 0)
                            q2 = 0;
                        y2 = y2 + 5 + k;
                        if (y2 > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = 1;
                            }
                            b2cp = 1;
                            myrak2 = 1;
                        }
                    }
                    if ((s + c) < x2 && x2 < (c + d) && y2 > ca.getHeight() - 20 && y2 < ca.getHeight()) {
                        myrak2 = 1;
                        try {
                            mp1.prepare();
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                        if (mp1.isPlaying()) {
                            mp1.seekTo(0);
                        }
                        mp1.start();
                        if (q2 == 0 && w2 == 0) {
                            w2 = 1;
                        }
                        if (q2 == 1 && w2 == 0) {
                            w2 = 1;
                        }
                    }
                    if (q2 == 1 && w2 == 1) {
                        x2 = x2 - 5 - k;
                        if (x2 < 0) {
                            q2 = 0;
                            w2 = 1;
                        }
                        y2 = y2 - 5 - k;
                        if (y2 < 20 && y2 > 0 && x2 < ca.getWidth() / 2 + 50 + cpux && x2 > ca.getWidth() / 2 - 50 + cpux) {
                            q2 = 1;
                            w2 = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y2 < 0) {
                            if (mypo == 0) {
                                mypo = 1;
                            }
                            b2my = 1;
                        }
                    }
                    if (q2 == 0 && w2 == 1) {
                        x2 = x2 + 5 + k;
                        if (x2 > ca.getWidth()) {
                            q2 = 1;
                            w2 = 1;
                        }
                        y2 = y2 - 5 - k;
                        if (y2 < 20 && y2 > 0 && x2 < ca.getWidth() / 2 + 50 + cpux && x2 > ca.getWidth() / 2 - 50 + cpux) {
                            q2 = 0;
                            w2 = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y2 < 0) {
                            if (mypo == 0) {
                                mypo = 1;
                            }
                            b2my = 1;
                        }
                    }
                }
                if (myrak2 == 1) {      //myrak2という変数で2個めのボールが弾かれたことを確認して3個めを動かします。
                    if (q3 == 0 && w3 == 0) {
                        x3 = x3 + 5 + k;
                        if (x3 > ca.getWidth())
                            q3 = 1;
                        y3 = y3 + 5 + k;
                        if (y3 > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = 1;
                            }
                            b3cp = 1;
                        }
                    }
                    if (q3 == 1 && w3 == 0) {
                        x3 = x3 - 5 - k;
                        if (x3 < 0)
                            q3 = 0;
                        y3 = y3 + 5 + k;
                        if (y3 > ca.getHeight()) {
                            if (cpupo == 0) {
                                cpupo = 1;
                            }
                            b3cp = 1;
                        }
                    }
                    if ((s + c) < x3 && x3 < (c + d) && y3 > ca.getHeight() - 20 && y3 < ca.getHeight()) {
                        try {
                            mp1.prepare();
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                        if (mp1.isPlaying()) {
                            mp1.seekTo(0);
                        }
                        mp1.start();            //効果音を鳴らしています。
                        if (q3 == 0 && w3 == 0) {
                            w3 = 1;
                        }
                        if (q3 == 1 && w3 == 0) {
                            w3 = 1;
                        }
                    }
                    if (q3 == 1 && w3 == 1) {
                        x3 = x3 - 5 - k;
                        if (x3 < 0) {
                            q3 = 0;
                            w3 = 1;
                        }
                        y3 = y3 - 5 - k;

                        if (y3 < 20 && y3 > 0 && x3 < ca.getWidth() / 2 + 50 + cpux && x3 > ca.getWidth() / 2 - 50 + cpux) {
                            q3 = 1;
                            w3 = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y3 < 0) {
                            if (mypo == 0) {
                                mypo = 1;
                            }
                            b3my = 1;
                        }
                    }
                    if (q3 == 0 && w3 == 1) {
                        x3 = x3 + 5 + k;
                        if (x3 > ca.getWidth()) {
                            q3 = 1;
                            w3 = 1;
                        }
                        y3 = y3 - 5 - k;
                        if (y3 < 20 && y3 > 0 && x3 < ca.getWidth() / 2 + 50 + cpux && x3 > ca.getWidth() / 2 - 50 + cpux) {
                            q3 = 0;
                            w3 = 0;
                            try {
                                mp1.prepare();
                            } catch (Exception e) {
                                e.printStackTrace();
                            }
                            if (mp1.isPlaying()) {
                                mp1.seekTo(0);
                            }
                            mp1.start();
                        }
                        if (y3 < 0) {
                            if (mypo == 0) {
                                mypo += 1;
                            }
                            b3my = 1;
                        }
                    }

                }
                if ((b1my == 1 && b2my == 1) || (b2my == 1 && b3my == 1) || (b3my == 1 && b1my == 1)) {     //勝った時のフラグ
                    katihuragu = 1;
                    if (cpuk == 18) {
                        cpuk = 19;      //コンピュータの性能を上げて難易度を高くしています。
                        k = 7;
                        kati11 = 1;
                    }
                }
                if ((b1cp == 1 && b2cp == 1) || (b2cp == 1 && b3cp == 1) || (b3cp == 1 && b1cp == 1)) {     //負けた時のフラグ
                    makehuragu = 1;
                }
                if (katihuragu == 1) {      //1回目に勝った時の処理
                    touch2 = 0;     //ボールやラケット、フラグを初期化します。
                    x = 300;
                    x2 = 300;
                    x3 = 300;
                    y = 300;
                    y2 = 300;
                    y3 = 300;
                    mypo = 0;
                    cpupo = 0;
                    b1my = 0;
                    b2my = 0;
                    b3my = 0;
                    b1cp = 0;
                    b2cp = 0;
                    b3cp = 0;
                    w = 0;
                    w2 = 0;
                    w3 = 0;
                    if (cpuk == 0) {
                        cpuk = 18;
                        k = 5;
                    }
                    myrak = 0;
                    myrak2 = 0;
                    kati1 = 1;
                    makehuragu = 0;
                }
                if (makehuragu == 1) {      //負けた場合完全な初期状態に戻しています。
                    touch2 = 0;
                    x = 300;
                    x2 = 300;
                    x3 = 300;
                    y = 300;
                    y2 = 300;
                    y3 = 300;
                    mypo = 0;
                    cpupo = 0;
                    b1my = 0;
                    b2my = 0;
                    b3my = 0;
                    b1cp = 0;
                    b2cp = 0;
                    b3cp = 0;
                    w = 0;
                    w2 = 0;
                    w3 = 0;
                    k = 2;
                    cpuk = 0;
                    myrak = 0;
                    myrak2 = 0;
                    kati1 = 1;
                    kati11 = 0;
                }
                pa3.setTextSize(100);
            }
                if (katihuragu == 0 && makehuragu == 0) {
                    if ((x == 300) && (y == 300) && y2 == 300 && y3 == 300 && x2 == 500 && x3 == 700) {
                        Bitmap bmt = BitmapFactory.decodeResource(getResources(), R.raw.lv12);
                        ca.drawBitmap(bmt, 100, 200, null);
                    } else {
                        ca.drawText(mypo + "-" + cpupo, ca.getWidth() / 2 - 60, ca.getHeight() / 2, pa3);
                    }
                } else if (katihuragu == 1) {
                    Bitmap bmp1 = BitmapFactory.decodeResource(getResources(), R.raw.lv22);
                    Bitmap bmp3 = BitmapFactory.decodeResource(getResources(), R.raw.lv32);
                    if (kati11 == 1) {
                        ca.drawBitmap(bmp3, 100, 200, null);
                    } else {
                        ca.drawBitmap(bmp1, 100, 200, null);
                    }
                    if (kati12 == 1) {
                        ca.drawBitmap(bmp3, 100, 200, null);
                    }
                } else {
                    Bitmap bmp2 = BitmapFactory.decodeResource(getResources(), R.raw.gameover44);
                    ca.drawBitmap(bmp2, 100, 200, null);
                }

            invalidate();
        }

        public boolean onTouchEvent(MotionEvent event) {        //画面をタッチしたことを感知して、難易度が変わった時にスタートする処理をするためのものです。
            if (event.getAction() == MotionEvent.ACTION_DOWN) {
                if (touch2 == 0) {
                    x = (int) (Math.random() * (getWidth() - 2) + 1);       //ボールの初期位置はある程度ランダムにしています。
                    y = (int) (Math.random() * getHeight() / 4 * (-1)) + getHeight() / 3;
                    q = (int) (Math.random() * 2);
                }
                if (touch2 == 0) {
                    x3 = (int) (Math.random() * (getWidth() - 2) + 1);
                    y2 = (int) (Math.random() * getHeight() / 4 * (-1)) + getHeight() / 3;
                    q2 = (int) (Math.random() * 2);
                }
                if (touch2 == 0) {
                    x3 = (int) (Math.random() * (getWidth() - 2) + 1);
                    y3 = (int) (Math.random() * getHeight() / 4 * (-1)) + getHeight() / 3;
                    q3 = (int) (Math.random() * 2);
                }
                if (touch2 == 0) {
                    if (katihuragu == 1) {
                        katihuragu = 0;
                        kati2 = 1;
                    }
                    if (makehuragu == 1) {
                        makehuragu = 0;
                    }
                }
                qq = 1;
            }
            if (event.getAction() == MotionEvent.ACTION_UP) {
                touch2 = touch2 + 1;
            }
            return true;
        }
    }

    public class CustomView extends View {
        public CustomView(Context context) {
            super(context);
        }
    }


    class SEL implements SensorEventListener {
        public void onSensorChanged(SensorEvent e) {
            if (e.sensor.getType() == Sensor.TYPE_ACCELEROMETER) {
                a_vals = e.values;
                cv.invalidate();
            }
        }
        public void onAccuracyChanged(Sensor se, int Accuracy) {
        }
    }
 }
