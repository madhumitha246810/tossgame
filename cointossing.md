#coin tossing- 
The winner was decided by the count of heads.
<!DOCTYPE html>
<html lang="en">

<head>
   <meta charset="UTF-8">
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Document</title>
</head>

<body>
   <script>
      score = {
         computer: 0,
         player: 0
      }
      c = []
      p = []
      totalpoints = []
      function tossing() {
         var cointoss = setInterval(game, 1000)
         toss = 0
         function game() {
            chances = ["head", "tail"]
            console.log("Toss", toss + 1)
            computer = chances[Math.floor(Math.random() * chances.length)]
            human = chances[Math.floor(Math.random() * chances.length)]
            c.push(computer)
            p.push(human)
            totalpoints.push({ "round": Round1, "computer": computer, "human": human })
            if (computer == "head") {
               score.computer += 1
            }
            if (human == "head") {
               score.player += 1
            }
            
            console.log("computer:", computer, "player:", human)
            toss++
            if (toss == 10) {
               clearInterval(cointoss);
               console.table(score)
               if (score.computer > score.player) {
                  console.log(`computer is leading player by ${score.computer-score.player}`)

               }
               else if (score.computer < score.player){
                score_player=score.player-score.computer
                console.log(`player is leading computer by ${score.player-score.computer}`)

               }
               else {
                  console.log("Computer and Player got same points")

               }
               
            }
         }
      }
      Round1 = 0
      var b = setInterval(function Round() {
         if (Round1 == 4) {
            clearInterval(b);
            console.table(totalpoints)
            csvExceldata()
           
        }
         else {
            console.log(`**********************************  Round-${Round1 + 1}  **********************************`)
            tossing()
            Round1++
            return Round
         }
      }(), 15000);

      function csvExceldata(){
                participant=""
                participant+="Round,computer,player"
                participant+="\r\n"
                result=0
            for (i of totalpoints) {
               participant += i.round + "," + i.computer + "," + i.human
               participant+="\r\n"
        
            }
            let tempBlob = new Blob([participant], { type: "text\csv" })
            let tempURL = window.URL.createObjectURL(tempBlob)
            let activation = document.createElement("a")
            activation.href = tempURL
            activation.download = "tossgame.csv"
            activation.click()
            window.URL.revokeObjectURL(tempURL)
            activation.remove()

         }


   </script>

</body>

</html>