# Android_Number_Guessing_Game
Simple number guessing game

# Code

#### 1st Activity 
```
 Button guessButton, refreshButton;
EditText editText;
TextView textView, tryRemaining;

int BOUND = 1000;
int TRY_COUNT = 10;

int randomNumber = 0;

//finding all the elements
guessButton = findViewById(R.id.guessButton);
refreshButton = findViewById(R.id.refreshButton);
editText = findViewById(R.id.editText);
textView = findViewById(R.id.textView);
tryRemaining = findViewById(R.id.tryRemaining);

        //Generating random number in the range of 1000
        generateRandomNumber();

        //showing hint to user (helps which range of number he/she have to guess)
        setHintOfNumberGenerated();
        
        guessButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                //get the guess of user and process according
                String userGuess = editText.getText().toString();
                if (!userGuess.equals("")) {
                    //String -> Int
                    int userGuessNo = Integer.parseInt(userGuess);

                    //Update UI
                    editText.setText("");
                    TRY_COUNT--;
                    tryRemaining.setText(TRY_COUNT + "");

                    //checking user left with guessing try
                    if (TRY_COUNT == 0) {

                        //show the dialog of loose and reset reset UI to default
                        new AlertDialog.Builder(MainActivity.this)
                                .setIcon(R.drawable.loose)
                                .setTitle("You Loose :(")
                                .setMessage("I was thinking of " + randomNumber + "\n\n\nDo you want to play again?")
                                .setPositiveButton("Yes!", new DialogInterface.OnClickListener() {
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        TRY_COUNT = 10;
                                        tryRemaining.setText(TRY_COUNT + "");

                                        //Generating random number in the range of 1000
                                        generateRandomNumber();

                                        //showing hint to user (helps which range of number he/she have to guess)
                                        setHintOfNumberGenerated();

                                        dialog.dismiss();
                                    }
                                })
                                .setNegativeButton("No", new DialogInterface.OnClickListener() {
                                    @Override
                                    public void onClick(DialogInterface dialog, int which) {
                                        textView.setText("Hello World!");
                                        tryRemaining.setText("10");
                                        guessButton.setVisibility(View.GONE);
                                        Toast.makeText(MainActivity.this, "Click Refresh Button To Start The Game Again!", Toast.LENGTH_SHORT).show();
                                        dialog.dismiss();
                                    }
                                })
                                .show();

                    } else {

                        //check the userGuess is the randomNumber
                        if (userGuessNo == randomNumber) {
                            //show the alert dialog of win
                            new AlertDialog.Builder(MainActivity.this)
                                    .setIcon(R.drawable.win)
                                    .setTitle("You Win!!")
                                    .setMessage("I am also thinking of " + randomNumber)
                                    .setPositiveButton("Hurray!", new DialogInterface.OnClickListener() {
                                        @Override
                                        public void onClick(DialogInterface dialog, int which) {
                                            dialog.dismiss();
                                        }
                                    }).show();

                            textView.setText(randomNumber + "");

                        } else if (userGuessNo > randomNumber)
                            Toast.makeText(MainActivity.this, userGuessNo + " is high :(", Toast.LENGTH_SHORT).show();
                        else if (userGuessNo < randomNumber)
                            Toast.makeText(MainActivity.this, userGuessNo + " is low :(", Toast.LENGTH_SHORT).show();
                    }
                } else
                    Toast.makeText(MainActivity.this, "Please guess a number", Toast.LENGTH_SHORT).show();
            }
        });

        refreshButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(MainActivity.this, "Game is Reset, Enjoy!", Toast.LENGTH_SHORT).show();

                guessButton.setVisibility(View.VISIBLE);

                TRY_COUNT = 10;
                tryRemaining.setText(TRY_COUNT + "");
                editText.setText("");

                //Generating random number in the range of 1000
                generateRandomNumber();

                //showing hint to user (helps which range of number he/she have to guess)
                setHintOfNumberGenerated();
            }
        });
    

    /**
     * Method will set the hint for the user
     * which says how many digit's number is generated
     */
    private void setHintOfNumberGenerated() {
        /*
        1 - 9 == ?
        10 - 99== ??
        100 - 999 == ???
        1000 == ????
         */
        String toSet = "";
        if (randomNumber < 10)
            toSet = "?";
        else if (randomNumber < 100)
            toSet = "??";
        else if (randomNumber < 1000)
            toSet = "???";
        else
            toSet = "????";

        //setting the hint in TextView
        textView.setText(toSet);
    }

    /**
     * Method to generate the random number
     * Random number will be generate every time the refresh button is clicked
     * or when the application is opened.
     */
    private void generateRandomNumber() {
        Random rd = new Random();
        randomNumber = rd.nextInt(BOUND) + 1; // 1 -> 1000
        Log.d("rd", "Number generated is :: " + randomNumber);
    }
```

# App Highlight

<img src="app_images/number guessing game code.png" width="1000" /><br>

<img src="app_images/number guessing game App1.png" width="300" /> <img src="app_images/number guessing game App2.png" width="300" /> <img src="app_images/number guessing game App3.png" width="300" /> <img src="app_images/number guessing game App4.png" width="300" /><br>

