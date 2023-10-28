<script>
    import ListToDo from "./DataStore";
    
        $: All = $ListToDo.length
        $: Done = $ListToDo.filter(t => t.status == true ).length
        $: NotDone = $ListToDo.filter(t => t.status == false ).length
    
    </script>
    
    <div>
    
    <p>{All} Всего заданий</p>
    <p>{Done} Выполнненых заданий</p>
    <p>{NotDone} Не выполненных заданий</p>
    
    </div>    