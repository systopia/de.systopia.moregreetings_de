# Beispiel für ein benutzerdefiniertes Grußformelfeld mit SMARTY

Hier sind zunächst einige Hinweise zum besseren Verständnis des vorliegenden Beispiels. Eine ausführliche Dokumentation und Referenz der SMARTY-Templating-Sprache finden Sie hier.

- SMARTY-Tags werden in der Regel von geschwungenen Klammern umschlossen. Standardmäßig sind dies { und }.
- Kommentare stehen zwischen "Sternchen". Sie werden in der Ausgabe nicht angezeigt.
- In SMARTY beginnen Variablen normalerweise mit einem Dollarzeichen $.
- SMARTY kann {if}-Anweisungen verwenden. Diese müssen mit einem passenden {/if} abgeschlossen werden. Es gibt die Möglichkeit, {else} hinzuzufügen, wenn die Bedingung nicht erfüllt ist, oder {elseif}, um eine weitere Testbedingung anzugeben.
- Der logische Operator ! gibt ein logisches Nicht an und bedeutet im Zusammenhang mit einer Variablen, dass die Bedingung erfüllt ist, wenn der Inhalt der Variablen leer ist (oder ein entsprechender Wert eines anderen Typs, z. B. 0 oder falsch).
- Der logische Operator && besagt, dass beide Ausdrücke wahr sein müssen, um die Bedingung zu erfüllen.
- Das Zeichen | bedeutet, dass SMARTY mehrere Funktionen kombiniert und sie nacheinander ausführt.

Im vorliegenden Beispiel prüft SMARTY zunächst den Kontakttyp (Haushalt, Organisation oder Einzelperson) des jeweiligen Kontaktes. Dann wird automatisch der Inhalt des entsprechenden Grußformelfeldes entsprechend der Prüfbedingungen generiert.

Besonders im Fall eines Einzelkontakts prüft Smarty mehrere Bedingungen ab. Anhand des Feldes Gender ID und des Feldes Prefix ID ermittelt SMARTY das Geschlecht des jeweiligen Kontakts und passt die Grußformel entsprechend an. Dann wird jeweils eine if-Bedingung verwendet, um den akademischen Titel zu prüfen und entsprechend an den Anfang der Grußformel zu platzieren.

Beachten Sie, dass es sich hier um ein Beispiel für deutsche Kontaktdaten handelt, wo sich die Endungen zwischen männlicher und weiblicher Anrede deutlich sprachlich unterscheiden.


```
{*prefix IDs: 5 --&gt; weiblich, 6 --&gt; maennlich*}
{*gender IDs: 1 --&gt; weiblich, 2 --&gt; maennlich, 3 --&gt;
unbestimmt, NULL*}
{*---------------------------------------------------*}

{if $contact.contact_type == 'Household'}
    Sehr geehrte Familie {$contact.last_name}

{elseif $contact.contact_type == 'Organization'}
    Sehr geehrte Damen und Herren

{else}
    
    {if !$contact.first_name && !$contact.last_name}
        {if $contact.formal_title|mg_startswith:'Prof'}
            Sehr geehrte/r Professor {$contact.first_name} {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'Dr'}
      	     Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'PD Dr'}
            Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
        {else}
            Sehr geehrte Damen und Herren
        {/if}
  
    {elseif !$contact.gender_id}
        {if $contact.prefix_id == '5'}
            {if $contact.formal_title|mg_startswith:'Prof'}
                Sehr geehrte Frau Professorin {$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'Dr'}
                Sehr geehrte Frau Dr. {$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'PD Dr'}
                Sehr geehrte Frau Dr. {$contact.last_name}
            {else}
               Sehr geehrte Frau {$contact.formal_title} {$contact.last_name}
        {/if}
    
	      {elseif $contact.prefix_id == '6'}
            {if $contact.formal_title|mg_startswith:'Prof'}
                Sehr geehrter Herr Professor {$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'Dr'}
                Sehr geehrter Herr Dr. {$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'PD Dr'}
                Sehr geehrte Herr Dr. {$contact.last_name}
            {else}
                Sehr geehrter Herr {$contact.formal_title} {$contact.last_name}
            {/if}
    
	      {else}
            {if $contact.formal_title|mg_startswith:'Prof'}
                Sehr geehrte/r Professor/in {$contact.first_name}
{$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'Dr'}
                Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
            {elseif $contact.formal_title|mg_startswith:'PD Dr'}
                Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
            {else}
                Sehr geehrte/r {$contact.formal_title} {$contact.first_name}
{$contact.last_name}
            {/if}
        {/if} 

    {elseif $contact.gender_id == '1'}
        {if $contact.formal_title|mg_startswith:'Prof'}
            Sehr geehrte Frau Professorin {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'Dr'}
            Sehr geehrte Frau Dr. {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'PD Dr'}
            Sehr geehrte Frau Dr. {$contact.last_name}
        {else}
            Sehr geehrte Frau {$contact.formal_title} {$contact.last_name}
        {/if}
  
    {elseif $contact.gender_id == '2'}
        {if $contact.formal_title|mg_startswith:'Prof'}
            Sehr geehrter Herr Professor {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'Dr'}
            Sehr geehrter Herr Dr. {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'PD Dr'}
            Sehr geehrte Herr Dr. {$contact.last_name}
        {else}
            Sehr geehrter Herr {$contact.formal_title} {$contact.last_name}
        {/if}

{*All other cases*}
    {else}
        {if $contact.formal_title|mg_startswith:'Prof'}
            Sehr geehrte/r Professor/in {$contact.first_name}
{$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'Dr'}
            Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
        {elseif $contact.formal_title|mg_startswith:'PD Dr'}
            Sehr geehrte/r Dr. {$contact.first_name} {$contact.last_name}
        {else}
            Sehr geehrte/r {$contact.formal_title} {$contact.first_name}
{$contact.last_name}
        {/if}
    {/if}
{/if}
```

Zum besseren Verständnis dieses Beispiels ist der Aufbau der Grußformel hier in Form einer Grafik dargestellt: ![graphic](/Images/Example_MoreGreetings.png)
