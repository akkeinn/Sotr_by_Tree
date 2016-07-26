using System;

namespace ConsoleApplication
{
    class Tree
    {
        // Значения узла дерева и его ветви
        private int value;
        private Tree left;
        private Tree right;
      
        public Tree( int value)
        {
            this.value = value;           
        }

        // Функция добавления элемента в дерево
        public void insert(Tree new_element)
        {
            if (new_element.value > value)
            {
                // Если элемент справа присутвует - рекурсивно запустить метод insert для правой ветви
                if (this.right != null)         
                {
                    right.insert(new_element);
                }
                else
                {
                    right = new_element;
                }
            }
            else
            {
                // Если элемент слева присутвует - рекурсивно запустить метод insert для левой ветви
                if (this.left != null)          
                {
                    left.insert(new_element);
                }
                else
                {
                    left = new_element;
                }
            }
        }

        // Метод записи дерева в массив
        public void Sort_all(ref int i, ref int[] Mass)
        {

            //  Сортировка левых ветвей дерева
            if (left != null)
            {
                left.Sort_all(ref i, ref Mass);
            }

            //  Запись отсортированных элементов во входной массив
            Mass[i++] = this.value;

            // Сортировка правых ветвей дерева
            if (right != null)
            {
                right.Sort_all(ref i, ref Mass);
            }
        }        
    }

        class Program
    {
        static void Main(string[] args)
        {
            //  Входный массив для сортировки
            int[] input_Massive = {26, 12, 25, 11, 1, 32, 98, 4, 5, 15, 6, 8, 91, 45, 16, 156, 0, +12, -51};

            //  Запуск сортировки массива 
            Sort_by_Tree(ref input_Massive);
            
            //  Вывод на экран
            for(int i=0;i<input_Massive.Length;i++)
                Console.Write(input_Massive[i]+" ");
            
            Console.Read();
        }
        
            // Функция сортировки
        static void Sort_by_Tree(ref int[] input_Massive)
        {
            //  Корневым узлом сортировки назначаем первый элемент массива
            Tree sorter = new Tree(input_Massive[0]);
            
            // Добавление всех элементов массива в дерево
            for (int i = 1; i<input_Massive.Length; i++)
                sorter.insert(new Tree(input_Massive[i]));

            int Count_Massive = 0;            
            // Сортировка массива
            sorter.Sort_all(ref Count_Massive, ref input_Massive);          
        }
    }
}
