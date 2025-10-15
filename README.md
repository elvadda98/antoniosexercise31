<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Life Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 154, 158, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #fff5f5);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #ff9a9e;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .word-bank h3 {
            color: #ff9a9e;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(255, 154, 158, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 154, 158, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #ff9a9e;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #ff9a9e;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #ff9a9e;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .option.selected {
            background: #ff9a9e;
            color: white;
            border-color: #ff9a9e;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #ff9a9e;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #ff9a9e;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .match-item.selected {
            background: #fff5f5;
            border-color: #ff9a9e;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 154, 158, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #ff9a9e;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #ff9a9e;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #ff9a9e;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-sun icon"></i> Vocabulary Game: Everyday Life Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff9a9e;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>sunset</h3>
                    <p><strong>Definition:</strong> The time in the evening when the sun disappears below the horizon.</p>
                    <p><strong>Usage:</strong> Describes the beautiful colors in the sky as day turns to night.</p>
                    <p class="example"><strong>Example:</strong> "We watched the beautiful sunset from the beach."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>meaning</h3>
                    <p><strong>Definition:</strong> The idea that is represented by a word, phrase, or symbol.</p>
                    <p><strong>Usage:</strong> What something expresses or represents.</p>
                    <p class="example"><strong>Example:</strong> "I don't understand the meaning of this word."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>understood</h3>
                    <p><strong>Definition:</strong> Past tense of understand; to have comprehended something.</p>
                    <p><strong>Usage:</strong> When you grasp the meaning or significance of something.</p>
                    <p class="example"><strong>Example:</strong> "After she explained it again, I finally understood the instructions."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>how do you feel</h3>
                    <p><strong>Definition:</strong> A question asking about someone's emotional or physical state.</p>
                    <p><strong>Usage:</strong> Used to inquire about emotions, health, or opinions.</p>
                    <p class="example"><strong>Example:</strong> "How do you feel about moving to a new city?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>outside</h3>
                    <p><strong>Definition:</strong> The external side or surface of something; not inside.</p>
                    <p><strong>Usage:</strong> Refers to the area beyond the confines of a building or space.</p>
                    <p class="example"><strong>Example:</strong> "The children are playing outside in the garden."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>hope</h3>
                    <p><strong>Definition:</strong> A feeling of expectation and desire for a particular thing to happen.</p>
                    <p><strong>Usage:</strong> Expressing optimism about future events.</p>
                    <p class="example"><strong>Example:</strong> "I hope you have a wonderful birthday."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>rubbish</h3>
                    <p><strong>Definition:</strong> Waste material; garbage or trash.</p>
                    <p><strong>Usage:</strong> Commonly used in British English for things to be discarded.</p>
                    <p class="example"><strong>Example:</strong> "Please take out the rubbish before you leave."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>bills</h3>
                    <p><strong>Definition:</strong> Statements of money owed for goods or services.</p>
                    <p><strong>Usage:</strong> Regular payments for utilities, rent, or services.</p>
                    <p class="example"><strong>Example:</strong> "I need to pay my electricity and water bills this week."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>luckily</h3>
                    <p><strong>Definition:</strong> In a lucky or fortunate manner; by good luck.</p>
                    <p><strong>Usage:</strong> Describing a fortunate circumstance or outcome.</p>
                    <p class="example"><strong>Example:</strong> "Luckily, I found my keys just before leaving the house."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>share</h3>
                    <p><strong>Definition:</strong> To have or use something at the same time as someone else.</p>
                    <p><strong>Usage:</strong> Dividing or distributing something among people.</p>
                    <p class="example"><strong>Example:</strong> "Would you like to share my umbrella?"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>careful</h3>
                    <p><strong>Definition:</strong> Giving attention or thought to what one is doing to avoid mistakes.</p>
                    <p><strong>Usage:</strong> Being cautious or attentive to prevent accidents or errors.</p>
                    <p class="example"><strong>Example:</strong> "Be careful when crossing the busy street."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>falling asleep</h3>
                    <p><strong>Definition:</strong> The process of beginning to sleep; transitioning from wakefulness to sleep.</p>
                    <p><strong>Usage:</strong> Describes the moment when someone starts sleeping.</p>
                    <p class="example"><strong>Example:</strong> "I had trouble falling asleep because of the noise outside."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>beard</h3>
                    <p><strong>Definition:</strong> The hair that grows on a man's chin and cheeks.</p>
                    <p><strong>Usage:</strong> Facial hair that some men grow and maintain.</p>
                    <p class="example"><strong>Example:</strong> "He decided to grow a beard during the winter months."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">sunset</span>
                    <span class="word-option">meaning</span>
                    <span class="word-option">understood</span>
                    <span class="word-option">how do you feel</span>
                    <span class="word-option">outside</span>
                    <span class="word-option">hope</span>
                    <span class="word-option">rubbish</span>
                    <span class="word-option">bills</span>
                    <span class="word-option">luckily</span>
                    <span class="word-option">share</span>
                    <span class="word-option">careful</span>
                    <span class="word-option">falling asleep</span>
                    <span class="word-option">beard</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff9a9e;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="sunset" onclick="selectMatch(this)">sunset</div>
                    <div class="match-item" data-word="meaning" onclick="selectMatch(this)">meaning</div>
                    <div class="match-item" data-word="understood" onclick="selectMatch(this)">understood</div>
                    <div class="match-item" data-word="how do you feel" onclick="selectMatch(this)">how do you feel</div>
                    <div class="match-item" data-word="outside" onclick="selectMatch(this)">outside</div>
                    <div class="match-item" data-word="hope" onclick="selectMatch(this)">hope</div>
                    <div class="match-item" data-word="rubbish" onclick="selectMatch(this)">rubbish</div>
                    <div class="match-item" data-word="bills" onclick="selectMatch(this)">bills</div>
                    <div class="match-item" data-word="luckily" onclick="selectMatch(this)">luckily</div>
                    <div class="match-item" data-word="share" onclick="selectMatch(this)">share</div>
                    <div class="match-item" data-word="careful" onclick="selectMatch(this)">careful</div>
                    <div class="match-item" data-word="falling asleep" onclick="selectMatch(this)">falling asleep</div>
                    <div class="match-item" data-word="beard" onclick="selectMatch(this)">beard</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What is a "sunset"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The time when the sun rises</div>
                    <div class="option" onclick="selectOption(this, true)">The time when the sun disappears below the horizon</div>
                    <div class="option" onclick="selectOption(this, false)">A type of flower</div>
                    <div class="option" onclick="selectOption(this, false)">A breakfast meal</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "meaning" refer to?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, true)">The idea represented by a word or phrase</div>
                    <div class="option" onclick="selectOption(this, false)">A feeling of happiness</div>
                    <div class="option" onclick="selectOption(this, false)">A mathematical calculation</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "understood" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To be confused about something</div>
                    <div class="option" onclick="selectOption(this, true)">To have comprehended something</div>
                    <div class="option" onclick="selectOption(this, false)">To forget information</div>
                    <div class="option" onclick="selectOption(this, false)">To disagree with someone</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: When would you ask "how do you feel"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">When asking for directions</div>
                    <div class="option" onclick="selectOption(this, true)">When asking about someone's emotional or physical state</div>
                    <div class="option" onclick="selectOption(this, false)">When ordering food at a restaurant</div>
                    <div class="option" onclick="selectOption(this, false)">When telling time</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "outside" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Inside a building</div>
                    <div class="option" onclick="selectOption(this, true)">The external side or surface; not inside</div>
                    <div class="option" onclick="selectOption(this, false)">Underground</div>
                    <div class="option" onclick="selectOption(this, false)">In the sky</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What is "hope"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A feeling of sadness</div>
                    <div class="option" onclick="selectOption(this, true)">A feeling of expectation for something to happen</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, false)">A mathematical concept</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What is "rubbish"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Something valuable</div>
                    <div class="option" onclick="selectOption(this, true)">Waste material; garbage or trash</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, false)">A precious metal</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What are "bills"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Types of birds</div>
                    <div class="option" onclick="selectOption(this, true)">Statements of money owed for goods or services</div>
                    <div class="option" onclick="selectOption(this, false)">Parts of a plant</div>
                    <div class="option" onclick="selectOption(this, false)">Musical instruments</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "luckily" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">In an unfortunate way</div>
                    <div class="option" onclick="selectOption(this, true)">In a lucky or fortunate manner</div>
                    <div class="option" onclick="selectOption(this, false)">With great effort</div>
                    <div class="option" onclick="selectOption(this, false)">Slowly and carefully</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What does "share" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To keep something for yourself</div>
                    <div class="option" onclick="selectOption(this, true)">To have or use something with others</div>
                    <div class="option" onclick="selectOption(this, false)">To hide something</div>
                    <div class="option" onclick="selectOption(this, false)">To destroy something</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What does "careful" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Reckless and hasty</div>
                    <div class="option" onclick="selectOption(this, true)">Giving attention to avoid mistakes</div>
                    <div class="option" onclick="selectOption(this, false)">Tired and sleepy</div>
                    <div class="option" onclick="selectOption(this, false)">Happy and excited</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 12: What is "falling asleep"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Waking up from sleep</div>
                    <div class="option" onclick="selectOption(this, true)">The process of beginning to sleep</div>
                    <div class="option" onclick="selectOption(this, false)">A type of exercise</div>
                    <div class="option" onclick="selectOption(this, false)">A cooking technique</div>
                </div>
                <div class="feedback" id="mc-feedback-12" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 13: What is a "beard"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Hair on top of the head</div>
                    <div class="option" onclick="selectOption(this, true)">Hair that grows on a man's chin and cheeks</div>
                    <div class="option" onclick="selectOption(this, false)">A type of plant</div>
                    <div class="option" onclick="selectOption(this, false)">A small animal</div>
                </div>
                <div class="feedback" id="mc-feedback-13" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "sunset", text: "The time when the sun disappears below the horizon" },
            { meaning: "meaning", text: "The idea represented by a word or phrase" },
            { meaning: "understood", text: "To have comprehended something" },
            { meaning: "how do you feel", text: "A question about emotional or physical state" },
            { meaning: "outside", text: "The external side; not inside" },
            { meaning: "hope", text: "A feeling of expectation for something to happen" },
            { meaning: "rubbish", text: "Waste material; garbage or trash" },
            { meaning: "bills", text: "Statements of money owed for goods or services" },
            { meaning: "luckily", text: "In a lucky or fortunate manner" },
            { meaning: "share", text: "To have or use something with others" },
            { meaning: "careful", text: "Giving attention to avoid mistakes" },
            { meaning: "falling asleep", text: "The process of beginning to sleep" },
            { meaning: "beard", text: "Hair that grows on a man's chin and cheeks" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "We watched the beautiful <input type='text' class='fill-blank' data-answer='sunset' placeholder='answer'> from the beach.", answer: "sunset" },
            { text: "I don't understand the <input type='text' class='fill-blank' data-answer='meaning' placeholder='answer'> of this word.", answer: "meaning" },
            { text: "After she explained it again, I finally <input type='text' class='fill-blank' data-answer='understood' placeholder='answer'> the instructions.", answer: "understood" },
            { text: "<input type='text' class='fill-blank' data-answer='how do you feel' placeholder='answer'> about moving to a new city?", answer: "how do you feel" },
            { text: "The children are playing <input type='text' class='fill-blank' data-answer='outside' placeholder='answer'> in the garden.", answer: "outside" },
            { text: "I <input type='text' class='fill-blank' data-answer='hope' placeholder='answer'> you have a wonderful birthday.", answer: "hope" },
            { text: "Please take out the <input type='text' class='fill-blank' data-answer='rubbish' placeholder='answer'> before you leave.", answer: "rubbish" },
            { text: "I need to pay my electricity and water <input type='text' class='fill-blank' data-answer='bills' placeholder='answer'> this week.", answer: "bills" },
            { text: "<input type='text' class='fill-blank' data-answer='luckily' placeholder='answer'>, I found my keys just before leaving the house.", answer: "luckily" },
            { text: "Would you like to <input type='text' class='fill-blank' data-answer='share' placeholder='answer'> my umbrella?", answer: "share" },
            { text: "Be <input type='text' class='fill-blank' data-answer='careful' placeholder='answer'> when crossing the busy street.", answer: "careful" },
            { text: "I had trouble <input type='text' class='fill-blank' data-answer='falling asleep' placeholder='answer'> because of the noise outside.", answer: "falling asleep" },
            { text: "He decided to grow a <input type='text' class='fill-blank' data-answer='beard' placeholder='answer'> during the winter months.", answer: "beard" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
