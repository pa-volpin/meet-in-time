# !/bin/bash

echo "Bem vindo(a) ao automatizador do dia! \o/"
echo ""
echo "Você pode agendar quantos meetings quiser em qualquer ordem!"
echo "1 - Insira o horário e o link de cada chamada"
echo "2 - Após inserir todos os meetings digite end"
echo ""
printf "Deseja ver um exemplo? (S/N):"
read seeExample
if [ $seeExample = "S" ]
then
  echo ""
  echo "----------------------------------------------------"
  echo "Horário: 1950 (// 19h50min)"
  echo "Link: https://trybe.zoom.us/j/95497239986"
  echo "Meeting configurado com sucesso!"
  echo "---"
  echo "Horário: 1640 (// 16h40min)"
  echo "Link: https://trybe.zoom.us/j/95497239986"
  echo "Meeting configurado com sucesso!"
  echo "---"
  echo "Horário: end"
  echo "Foram configurados 2 meetings! Bons estudos!"
  echo "----------------------------------------------------"
  echo ""
fi

echo ""
echo "Para colar o link use CTRL + SHIFT + V. Let's go!"
echo ""



hour=$(date +%H%M)
schedule="oo"
link="oo"
i=0
while [ $schedule != "end" ]
do
  printf "Horário: "
  read schedule
  if [ $schedule != "end" ]
  then
    printf "Link: "
    read link
    echo "Meeting configurado com sucesso!"
    echo "---"
    var=$(($schedule + 0))
    schedules[$i]=$var
    linksId[$i]="$(echo $link | awk -F'https://trybe.zoom.us/j/' '{print $2}')"
    i=$((i+1))
  else
    if [ $i -ne 0 ]
      then
        if [ $i -eq 1 ]
        then
          echo "Foi configurado $i meeting! Não feche o terminal! Bons estudos!"
        else
          echo "Foram configurados $i meetings! Não feche o terminal! Bons estudos!" 
        fi
    fi
  fi
done

# Performing Bubble sort  
len=${#schedules[@]}
for ((i = 0; i<len; i++)) 
do
    for((j = 0; j<len-i-1; j++)) 
    do    
        if [ ${schedules[j]} -gt ${schedules[$((j+1))]} ] 
        then
            # swap 
            # schedules
            temp=${schedules[j]} 
            schedules[$j]=${schedules[$((j+1))]}   
            schedules[$((j+1))]=$temp 
            # Meeting Ids
            tempLink=${linksId[j]} 
            linksId[$j]=${linksId[$((j+1))]}   
            linksId[$((j+1))]=$tempLink
        fi
    done
done

len=${#schedules[@]}
hour=0
for ((i = 0; i<len; i++)) 
do
  while [ $hour -ne ${schedules[$i]} ]
  do
    d=$(date +%H%M)
    hour=$(($d + 0))
  done
  xdg-open "zoommtg://zoom.us/join?action=join&confno=${linksId[$i]}"
done