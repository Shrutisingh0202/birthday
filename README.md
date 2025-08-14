<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Define custom fonts */
        body {
            font-family: 'Poppins', sans-serif;
            /* Giggles, upload your BACKGROUND image to postimages.org and paste the DIRECT link here! */
            background-image: url('https://i.pinimg.com/736x/46/18/11/461811bcc4b6831a4c0440d7309f27a2.jpg');
            background-color: #ffffff; /* White fallback color */
            background-size: cover;
            background-attachment: fixed; /* Keeps the background still while scrolling */
            background-position: center;
        }

        .font-pacifico {
            font-family: 'Pacifico', cursive;
        }

        /* Style for the content sections to fade in */
        .content-section, .letter-page, .reason-page, .coupon-page {
            display: none;
            animation: fadeIn 0.8s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Styles for the Password Modal */
        .modal-overlay {
            display: none;
            position: fixed;
            z-index: 100;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.5);
            backdrop-filter: blur(4px);
            animation: fadeIn 0.3s;
        }

        .modal-content {
            animation: slideIn 0.4s;
        }
        
        @keyframes slideIn {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* Styles for the Image Pop-up Messages */
        @keyframes pop-in-out {
            0% { transform: scale(0.8); opacity: 0; }
            20% { transform: scale(1.05); opacity: 1; }
            80% { transform: scale(1); opacity: 1; }
            100% { transform: scale(0.9); opacity: 0; } /* Removed the blur */
        }

        .popup-animation {
            display: flex;
            animation: pop-in-out 3s ease-in-out forwards; /* Changed duration to 3s */
        }
    </style>
</head>
<body class="text-gray-800">

    <!-- Password Modal -->
    <div id="password-modal" class="modal-overlay justify-center items-center">
        <div class="modal-content bg-white p-8 rounded-2xl shadow-2xl w-11/12 max-w-sm text-center">
            <h3 class="font-pacifico text-3xl text-red-600 mb-4">Password Required</h3>
            <p id="hint-text" class="text-gray-600 mb-4">Hint: [Hint will appear here]</p>
            <input id="password-input" type="password" placeholder="Enter password..." class="w-full p-3 border-2 border-gray-300 rounded-lg text-center focus:border-red-500 focus:outline-none">
            <div class="flex gap-4 mt-4">
                <button onclick="closeModal()" class="w-full bg-gray-300 text-gray-800 font-bold py-3 px-6 rounded-full hover:bg-gray-400 transition">Cancel</button>
                <button id="submit-password-btn" class="w-full bg-red-600 text-white font-bold py-3 px-6 rounded-full hover:bg-red-700 transition">Unlock</button>
            </div>
        </div>
    </div>
    
    <!-- Success Message Pop-up -->
    <div id="success-message" class="hidden fixed inset-0 z-[110] justify-center items-center pointer-events-none">
        <!-- Giggles, put your GOOD JOB cat image link here! -->
        <img src="https://i.postimg.cc/L6gWXgD9/Screenshot-2025-08-14-150911.png" alt="GOOD JOB BABY" class="rounded-2xl shadow-2xl max-w-s">
    </div>

    <!-- Error Message Pop-up -->
    <div id="error-message" class="hidden fixed inset-0 z-[110] justify-center items-center pointer-events-none">
        <!-- Giggles, put your WRONG PASSWORD cat image link here! -->
        <img src="https://i.postimg.cc/HxpQqRZc/Screenshot-2025-08-14-150559.png" alt="Try Again!" class="rounded-2xl shadow-2xl max-w-s">
    </div>

    <!-- Main Container -->
    <div class="container mx-auto p-4 md:p-8 max-w-4xl">

        <!-- Initial Welcome Screen -->
        <div id="welcome-screen" class="text-center min-h-screen flex flex-col justify-center items-center">
            <div class="bg-white/80 backdrop-blur-sm p-8 rounded-2xl shadow-2xl">
                <h1 class="font-pacifico text-5xl md:text-8xl text-red-600 drop-shadow-lg">Happy Birthday Baby!</h1>
                <p class="mt-8 text-lg md:text-2xl text-gray-600">I made a little something for you...</p>
                <button onclick="showMainMenu()" class="mt-8 bg-red-600 text-white font-bold py-3 px-8 rounded-full shadow-lg hover:bg-red-700 transition-transform transform hover:scale-105">
                    Surprise!
                </button>
            </div>
        </div>

        <!-- Main Content Menu (hidden initially) -->
        <div id="main-menu" style="display: none;">
            <header class="text-center py-8 bg-white/80 backdrop-blur-sm rounded-2xl shadow-2xl">
                <h2 class="font-pacifico text-4xl md:text-6xl text-red-600">Your Surprises</h2>
                <p class="text-gray-600 mt-2">Choose what you want to see first!</p>
            </header>
            <nav class="grid grid-cols-2 md:grid-cols-4 gap-4 my-8">
                <!-- Giggles, change the passwords and hints here! -->
                <button onclick="promptForPassword('reason-1', '170806', 'Hint: YOUR BIRTHDAY (DDMMYY)?')" class="bg-white p-4 rounded-xl shadow-md hover:shadow-xl transition-shadow text-red-600 font-semibold">💖 3 Reasons</button>
                <button onclick="promptForPassword('letters-menu', 'love', 'Hint: I ____ YOU!')" class="bg-white p-4 rounded-xl shadow-md hover:shadow-xl transition-shadow text-red-600 font-semibold">💌 Letters For You</button>
                <button onclick="promptForPassword('coupons-menu', 'one', 'Hint: How many girlfriends do you have?')" class="bg-white p-4 rounded-xl shadow-md hover:shadow-xl transition-shadow text-red-600 font-semibold">🎟️ Coupon Book</button>
                <button onclick="promptForPassword('edits-menu', '020206', 'Hint: MY BIRTHDAY (DDMMYY)')" class="bg-white p-4 rounded-xl shadow-md hover:shadow-xl transition-shadow text-red-600 font-semibold">🎬 Our Edits</button>
            </nav>
        </div>

        <!-- Container for the dynamic content sections -->
        <main id="sections-container">

            <!-- "3 Reasons" Step-by-Step Reveal -->
            <section id="reason-1" class="reason-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg text-center">
                 <button onclick="showMainMenu()" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Surprises</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6">Reason #1</h3>
                <p class="text-2xl mb-8">I love how you don't just call me your princess, but you actually treat me like one.</p>
                <button onclick="showSection('reason-2')" class="bg-red-600 text-white font-bold py-2 px-6 rounded-full shadow-lg hover:bg-red-700 transition">Next Reason &rarr;</button>
            </section>

            <section id="reason-2" class="reason-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg text-center">
                <h3 class="font-pacifico text-3xl text-red-600 mb-6">Reason #2</h3>
                <p class="text-2xl mb-8">I love the way you hug me.</p>
                <button onclick="showSection('reason-3')" class="bg-red-600 text-white font-bold py-2 px-6 rounded-full shadow-lg hover:bg-red-700 transition">And the third is... &rarr;</button>
            </section>

            <section id="reason-3" class="reason-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg text-center">
                <h3 class="font-pacifico text-3xl text-red-600 mb-6">Reason #3</h3>
                <p class="text-2xl mb-8">I love how crazy you are to think that there are only 3 things, here's 100 more...</p>
                <button onclick="showSection('reasons-full-list')" class="bg-red-600 text-white font-bold py-2 px-6 rounded-full shadow-lg hover:bg-red-700 transition">See the real list...</button>
            </section>

            <section id="reasons-full-list" class="reason-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                 <button onclick="showMainMenu()" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Surprises</button>
                 <div class="space-y-6">
                    <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">The Little Things...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="4">
                            <li>The way your eyes light up when you're excited.</li>
                            <li>How you're always ready to do a silly trend with me.</li>
                            <li>Your terrible dancing (it's my favorite).</li>
                            <li>The way you listen to me, really listen.</li>
                            <li>How you always find excuses to pick me up.</li>
                            <li>The sound of your voice on the phone.</li>
                            <li>The way you say my name.</li>
                            <li>How you physically cannot say no to me.</li>
                            <li>Your random bursts of energy.</li>
                            <li>The face you make when you're concentrating.</li>
                            <li>How you don't let me even touch any door and hold them open for me.</li>
                            <li>The way you hold my hand even when you have 100 things in your hand.</li>
                            <li>Your weirdly perfect sense of direction.</li>
                            <li>How you sing along to songs, even if you don't know the words.</li>
                        </ol>
                    </div>
                    <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">How You Make Me Feel...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="18">
                            <li>How safe I feel in your arms.</li>
                            <li>How you make me laugh.</li>
                            <li>The way you make me feel beautiful.</li>
                            <li>How you calm me down when I'm anxious.</li>
                            <li>You make me feel like I can do anything.</li>
                            <li>How you make boring things feel fun.</li>
                            <li>The butterflies I still get when you look at me.</li>
                            <li>You make me feel completely understood.</li>
                            <li>How you make me a better person.</li>
                            <li>The feeling of home I get when I'm with you.</li>
                            <li>How you make me feel cherished.</li>
                            <li>You make me feel brave.</li>
                            <li>How you make me feel like the only girl in the room.</li>
                        </ol>
                    </div>
                    <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">Things I Admire About You...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="31">
                            <li>Your kindness to people.</li>
                            <li>Your ambition and your drive.</li>
                            <li>Your intelligence. You're so smart.</li>
                            <li>Your weird sense of humor.</li>
                            <li>Your charm.</li>
                            <li>Your patience with me.</li>
                            <li>The way you support me.</li>
                            <li>The way you protect the people you love.</li>
                            <li>How honest you are.</li>
                            <li>Your strength, both inside and out.</li>
                            <li>How it's physically hard for you to lie.</li>
                            <li>Your loyalty.</li>
                            <li>The respect you show to others.</li>
                        </ol>
                    </div>
                     <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">Our Memories Together...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="44">
                            <li>That time in the metro when we thought it was our last day.</li>
                            <li>The first time i held your hand in the movie theatre.</li>
                            <li>All the times we've laughed endlessly about nothing.</li>
                            <li>Our late-night talks that last for hours.</li>
                            <li>That time I tickled your bum and you laughed so hard.</li>
                            <li>Our first date.</li>
                            <li>Every silly selfie we've ever taken.</li>
                            <li>The time you put your warm hands on my tummy to make me feel better.</li>
                            <li>Travelling in metro with music in our ears.</li>
                            <li>Our adventures day in EOD.</li>
                            <li>Cooking together (especially when you made gol gol poori).</li>
                            <li>The first time you called me your princess.</li>
                        </ol>
                    </div>
                     <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">Just Because...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="56">
                            <li>Your smile.</li>
                            <li>The sound of your laugh.</li>
                            <li>Your eyes.</li>
                            <li>Your hands.</li>
                            <li>The way you look when you've just woken up.</li>
                            <li>Your hugs from behind.</li>
                            <li>Your hugs from the front.</li>
                            <li>The way you look at me when you think I'm not looking.</li>
                            <li>Your taste in movies.</li>
                            <li>How you're always up for an adventure.</li>
                            <li>The way you smell.</li>
                            <li>How you make me feel like the most important person in the world.</li>
                            <li>Your little quirks that no one else sees.</li>
                            <li>How you can be serious one moment and a complete goofball the next.</li>
                            <li>Your sleepy and deep voice in the morning.</li>
                            <li>How you're my best friend.</li>
                            <li>The way you can always find the silver lining.</li>
                            <li>Your quick wit.</li>
                            <li>How you're always challenging me to think differently.</li>
                            <li>Your endless curiosity about the world.</li>
                            <li>The way you solve problems.</li>
                            <li>Your incredible memory (maybe).</li>
                            <li>Your perspective on life.</li>
                            <li>How you're never afraid to be wrong and learn.</li>
                        </ol>
                    </div>
                    <div>
                        <h4 class="font-pacifico text-2xl text-red-500 mb-2">And For Our Future...</h4>
                        <ol class="list-decimal list-inside space-y-1 text-left" start="81">
                            <li>The thought of all the adventures we still have to go on.</li>
                            <li>How excited I am to build a future with you.</li>
                            <li>Picturing us growing old together.</li>
                            <li>The thought of all the new inside jokes we'll create.</li>
                            <li>How I know you'll be an amazing husband one day.</li>
                            <li>The thought of celebrating a lifetime of birthdays with you.</li>
                            <li>How I know we can get through anything together.</li>
                            <li>Dreaming about the home we'll make.</li>
                            <li>The thought of all the new "firsts" we have yet to experience.</li>
                            <li>How you make me feel so hopeful for the future.</li>
                            <li>Knowing I'll always have you to lean on.</li>
                            <li>The thought of continuing to grow and learn with you.</li>
                            <li>How I can't wait to see what the next chapter holds for us.</li>
                            <li>Knowing that with you, the best is always yet to come.</li>
                            <li>That I get to love you.</li>
                            <li>That I get to be loved by you.</li>
                            <li>I love you.</li>
                            <li>I love you.</li>
                            <li>I love you.</li>
                            <li>And I'll love you forever.</li>
                        </ol>
                    </div>
                 </div>
            </section>

            <!-- Section 2: Letters Menu -->
            <section id="letters-menu" class="content-section bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showMainMenu()" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Surprises</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">Letters For You</h3>
                <div class="space-y-4">
                    <button onclick="showLetter('letter-birthday')" class="w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">Happy Birthday AJ</button>
                    <button onclick="showLetter('letter-bad-day')" class="w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">Open when... you've had a bad day</button>
                    <button onclick="showLetter('letter-laugh')" class="w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">Open when... you need a laugh</button>
                </div>
            </section>

            <!-- Individual Letter Pages -->
            <section id="letter-birthday" class="letter-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('letters-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Letters</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">Happy Birthday AJ</h3>
                <p class="text-gray-700 leading-relaxed">To my amazing boyfriend,<br><br>Happy birthday! I've been trying to think of the perfect words to tell you how much you mean to me, and I keep coming back to the little things.<br><br>Like the fact that you physically cannot say no to me (don't worry, I promise to only use this power for good... mostly). Or how you're always ready to do any silly trend, especially the ones that require you to pick me up—it makes me feel like the main character every single time.<br><br>But it's not just the funny things. It's the deep-down, good-hearted things, too. It's the way I see you being so genuinely kind to people when you think no one's watching. It's how you don't just call me your princess, you actually treat me like one, every single day. And it's the way you hug me—that perfect, all-encompassing hug that makes the whole world disappear.<br><br>I absolutely love everything about you... well, *almost* everything. We can talk about your [insert a funny, harmless flaw here] later.<br><br>For today, just know that you are my favorite person, and I'm the luckiest girl in the world to be celebrating with you.<br><br>All my love, always,<br>Shruti</p>
            </section>

            <section id="letter-bad-day" class="letter-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('letters-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Letters</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">A Letter For When You've Had a Bad Day</h3>
                <p class="text-gray-700 leading-relaxed">My love,<br><br>Okay, first things first: take a deep breath. Whatever happened today, I promise it's not as big as the universe and definitely not as important as you are to me.<br><br>I know on days like this your brain can go into overdrive, so let me just remind you of the official, undisputed facts: You are <strong>smart</strong> (even when you feel like you're not), you are <strong>funny</strong> (even when you don't feel like smiling), and you are ridiculously <strong>cute</strong> (that one's non-negotiable, sorry). It's a dangerous combination, really.<br><br>I know your go-to comfort is talking to me, and my line is always, always open for you. We can dissect the entire day, or we can talk about complete nonsense until you forget what was bothering you in the first place. Your call.<br><br>And if you need a smile, just think about that time in the movie theatre. Remember when I held your hand and you blushed so hard I could practically feel the heat coming off you in the dark? Thinking about that still makes my heart do a little flip.<br><br>This day does not define you. You're my favorite person, and you've got this.<br><br>Always here for you,<br>Shruti</p>
            </section>

            <section id="letter-laugh" class="letter-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('letters-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Letters</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">A Letter For When You Need a Laugh</h3>
                <p class="text-gray-700 leading-relaxed">Hey you,<br><br>Is the world being a bit too serious today? Let's fix that.<br><br>I was just thinking about that time we were in the metro, and that person threw their bag in right as the doors were closing. I swear, for a solid second, we both thought, 'well, last day ig!' The way we went from pure panic to laughing so hard we couldn't breathe is one of my favorite memories. We have so many moments like that, where we just laugh endlessly.<br><br>And it's not always the grand, dramatic stuff. Sometimes it's as simple as me tickling your bum and hearing you laugh that completely makes my day.<br><br>Thank you for being the person I share all my laughter with. There's no better sound than yours.<br><br>Love you,<br>Shruti</p>
            </section>
            
            <!-- Section 3: Coupon Book Menu -->
            <section id="coupons-menu" class="content-section bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showMainMenu()" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Surprises</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">Your Coupon Book</h3>
                <p class="text-center mb-6 text-gray-600">Click a card to reveal your coupon!</p>
                <div class="grid grid-cols-2 gap-6">
                    <button onclick="showCoupon('coupon-kiss')" class="bg-red-50 border-2 border-red-300 rounded-lg p-4 flex flex-col items-center justify-center aspect-square text-center hover:bg-red-100 transition">
                        <div class="text-5xl">😘</div>
                        <h4 class="font-pacifico text-xl text-red-700 mt-2">Kiss Card</h4>
                    </button>
                    <button onclick="showCoupon('coupon-win')" class="bg-red-50 border-2 border-red-300 rounded-lg p-4 flex flex-col items-center justify-center aspect-square text-center hover:bg-red-100 transition">
                        <div class="text-5xl">🏆</div>
                        <h4 class="font-pacifico text-xl text-red-700 mt-2">Win Pass Card</h4>
                    </button>
                    <button onclick="showCoupon('coupon-getoutoftrouble')" class="bg-red-50 border-2 border-red-300 rounded-lg p-4 flex flex-col items-center justify-center aspect-square text-center hover:bg-red-100 transition">
                        <div class="text-5xl">🙊</div>
                        <h4 class="font-pacifico text-xl text-red-700 mt-2">Get Out Of Trouble Free</h4>
                    </button>
                    <button onclick="showCoupon('coupon-yesday')" class="bg-red-50 border-2 border-red-300 rounded-lg p-4 flex flex-col items-center justify-center aspect-square text-center hover:bg-red-100 transition">
                        <div class="text-5xl">👍</div>
                        <h4 class="font-pacifico text-xl text-red-700 mt-2">The "Yes Day" Card</h4>
                    </button>
                </div>
            </section>

            <!-- Individual Coupon Pages -->
            <section id="coupon-kiss" class="coupon-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('coupons-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Cards</button>
                <div class="bg-red-50 border-2 border-dashed border-red-300 rounded-lg p-8 flex flex-col items-center text-center">
                    <h4 class="font-pacifico text-3xl text-red-700">Spontaneous Kiss</h4>
                    <p class="text-gray-600 my-4 text-lg">Redeem this coupon at any random moment for one big, spontaneous kiss.</p>
                    <p class="text-sm text-red-400 mt-auto">Expires: 17.08.2026</p>
                </div>
            </section>
            <section id="coupon-win" class="coupon-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('coupons-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Cards</button>
                <div class="bg-red-50 border-2 border-dashed border-red-300 rounded-lg p-8 flex flex-col items-center text-center">
                    <h4 class="font-pacifico text-3xl text-red-700">"You Win" Pass</h4>
                    <p class="text-gray-600 my-4 text-lg">This coupon can be used to instantly win any one (1) argument. Use it wisely!</p>
                    <p class="text-sm text-red-400 mt-auto">Expires: 17.08.2026</p>
                </div>
            </section>
            <section id="coupon-getoutoftrouble" class="coupon-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('coupons-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Cards</button>
                <div class="bg-red-50 border-2 border-dashed border-red-300 rounded-lg p-8 flex flex-col items-center text-center">
                    <h4 class="font-pacifico text-3xl text-red-700">Get Out Of Trouble Free</h4>
                    <p class="text-gray-600 my-4 text-lg">This card is a one-time pass to get out of trouble for a minor offense. (Note: Does not apply to major crimes against homosapiens or forgetting important dates).</p>
                    <p class="text-sm text-red-400 mt-auto">Expires: 17.08.2026</p>
                </div>
            </section>
            <section id="coupon-yesday" class="coupon-page bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showSection('coupons-menu')" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Cards</button>
                <div class="bg-red-50 border-2 border-dashed border-red-300 rounded-lg p-8 flex flex-col items-center text-center">
                    <h4 class="font-pacifico text-3xl text-red-700">The "Yes Day" Card</h4>
                    <p class="text-gray-600 my-4 text-lg">Redeem this and I have to say 'YES' to the next three things you ask for. (Please be nice!)</p>
                    <p class="text-sm text-red-400 mt-auto">Expires: 17.08.2026</p>
                </div>
            </section>

            <!-- Section 4: Our Edits Menu -->
            <section id="edits-menu" class="content-section bg-white/90 backdrop-blur-sm p-6 md:p-8 rounded-2xl shadow-lg">
                <button onclick="showMainMenu()" class="mb-8 bg-gray-200 text-gray-800 font-bold py-2 px-4 rounded-full hover:bg-gray-300 transition">&larr; Back to Surprises</button>
                <h3 class="font-pacifico text-3xl text-red-600 mb-6 text-center">Our Edits</h3>
                <p class="text-center mb-4">Click on an edit you wanna watch first!</p>
                <div class="space-y-4">
                    <!-- Giggles, get the shareable link from Google Drive ("Anyone with the link") and paste it here! -->
                    <a href="https://drive.google.com/file/d/1uq4n-QjuwhUkWIfcKATYP28SRC7OgWr4/view?usp=drive_link" target="_blank" class="block w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">
                        HAPPY BIRTHDAY LOVE!
                    </a>
                    <a href="YOUR_GOOGLE_DRIVE_LINK_HERE_2" target="_blank" class="block w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">
                        Pt. 2
                    </a>
                    <a href="YOUR_GOOGLE_DRIVE_LINK_HERE_3" target="_blank" class="block w-full text-left bg-red-50 p-4 rounded-lg font-bold text-lg text-red-700 hover:bg-red-100 transition">
                        Pt. 3
                    </a>
                </div>
            </section>
        </main>
    </div>

    <script>
        // --- JavaScript for interactivity ---
        const welcomeScreen = document.getElementById('welcome-screen');
        const mainMenu = document.getElementById('main-menu');
        const allSections = document.querySelectorAll('.content-section, .letter-page, .reason-page, .coupon-page');
        const modal = document.getElementById('password-modal');
        const hintText = document.getElementById('hint-text');
        const passwordInput = document.getElementById('password-input');
        const submitBtn = document.getElementById('submit-password-btn');
        const successMessage = document.getElementById('success-message');
        const errorMessage = document.getElementById('error-message');

        let currentSectionId = '';
        let currentPassword = '';
        let currentHint = '';

        function hideAll() {
            welcomeScreen.style.display = 'none';
            mainMenu.style.display = 'none';
            allSections.forEach(section => {
                section.style.display = 'none';
            });
        }

        function showMainMenu() {
            hideAll();
            mainMenu.style.display = 'block';
        }

        function showSection(sectionId) {
            hideAll();
            const activeSection = document.getElementById(sectionId);
            if (activeSection) {
                activeSection.style.display = 'block';
            }
        }

        function showLetter(letterId) {
             hideAll();
            const activeLetter = document.getElementById(letterId);
            if (activeLetter) {
                activeLetter.style.display = 'block';
            }
        }

        function showCoupon(couponId) {
             hideAll();
            const activeCoupon = document.getElementById(couponId);
            if (activeCoupon) {
                activeCoupon.style.display = 'block';
            }
        }

        function promptForPassword(sectionId, password, hint) {
            currentSectionId = sectionId;
            currentPassword = password.toLowerCase();
            currentHint = hint;
            hintText.textContent = hint;
            passwordInput.value = '';
            modal.style.display = 'flex';
            passwordInput.focus();
        }

        function closeModal() {
            modal.style.display = 'none';
        }

        function checkPassword() {
            const enteredPassword = passwordInput.value.toLowerCase();
            if (enteredPassword === currentPassword) {
                closeModal();
                
                // Show success message with animation
                successMessage.classList.add('popup-animation');
                successMessage.classList.remove('hidden');

                // Wait for the animation to finish, then show the content
                setTimeout(() => {
                    successMessage.classList.remove('popup-animation');
                    successMessage.classList.add('hidden');
                    showSection(currentSectionId);
                }, 3000); // Duration of the animation (3s)

            } else {
                closeModal();

                // Show error image with animation
                errorMessage.classList.add('popup-animation');
                errorMessage.classList.remove('hidden');

                // Wait for animation, then re-prompt for password
                setTimeout(() => {
                    errorMessage.classList.remove('popup-animation');
                    errorMessage.classList.add('hidden');
                    promptForPassword(currentSectionId, currentPassword, currentHint);
                }, 3000); // Duration of the animation (3s)
            }
        }

        submitBtn.addEventListener('click', checkPassword);
        passwordInput.addEventListener('keyup', function(event) {
            if (event.key === "Enter") {
                checkPassword();
            }
        });

    </script>
</body>
</html>
